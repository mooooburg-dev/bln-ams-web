<template>
    <div class="container-main">
        <div>
            <h2>Belluno AMS</h2>
        </div>
        <div class="search-area">
            <table class="search-table" style="width:100%; height:80px;">
                <colgroup>
                    <col width=29%>
                    <col width=54%>
                    <col width=17%>
                </colgroup>
                <tr>
                    <td>
                        <div class="search-cate">
                            <div class="form-check">
                                <b-form-radio class="radio-cate" v-model="selected_cate" name="some-radios" value="0">전체</b-form-radio>
                                <b-form-radio class="radio-cate" v-model="selected_cate" name="some-radios" value="1">검색 기간</b-form-radio>
                                <b-form-radio class="radio-cate" v-model="selected_cate" name="some-radios" value="2">기준 일</b-form-radio>
                            </div>
                        </div>
                    </td>
                    <td>
                        <div v-if="selected_cate == '0'">
                            
                        </div>
                        <div v-if="selected_cate == '1'">
                            <table class="search-table">
                                <tr>
                                    <td>검색 기간</td>
                                    <td><input type="Start Date" class="form-control date-input" id="Start Data"></td>
                                    <td> ~ </td>
                                    <td><input type="End Date" class="form-control date-input" id="End Date"></td>
                                </tr>
                            </table>
                        </div>
                        <div v-if="selected_cate == '2'">
                            <table class="search-table">
                                <tr>
                                    <td>기준 일</td>
                                    <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                </tr>
                            </table>
                        </div>
                    </td>
                    <td style="text-align:right;">
                        <div class="btn-wrap">
                            <button type="button" class="btn btn-info">Search</button>
                            <b-button v-b-modal.modal-input class="btn btn-info">Write</b-button>

                            <b-modal id="modal-input" size="lg" title="Input Data" @show="resetModal" @hidden="resetModal" @ok="handleOk">
                                <table class="input-table" style="width:100%;">
                                    <tr>
                                        <td></td>
                                        <td>날짜</td>
                                        <td>내용</td>
                                        <td>수입</td>
                                        <td>지출</td>
                                    </tr>
                                    <tr>
                                        <td>1</td>
                                        <td><input type="text" class="form-control" id="input-date" v-model="input_date" placeholder="(yyyymmdd)" maxlength="8"></td>
                                        <td><input type="text" class="form-control" id="input-title" v-model="input_title" placeholder="title"></td>
                                        <td><input type="text" class="form-control" id="input-income" v-model="input_income" placeholder="0"></td>
                                        <td><input type="text" class="form-control" id="input-paid" v-model="input_paid" placeholder="0"></td>
                                    </tr>
                                </table>
                            </b-modal>
                        </div>
                    </td>
                </tr>
            </table>
            
        </div>
        <div class="main-table-wrapper">
            <table class="table table-bordered main-table" border="1">
                <colgroup>
                    <col width="25%">
                    <col width="25%">
                    <col width="25%">
                    <col width="25%">
                </colgroup>
                <thead class="thead-dark">
                    <th>날짜</th>
                    <th>내용</th>
                    <th>수입</th>
                    <th>지출</th>
                </thead>
                <tr :v-for="item in data[0]">
                    <td>{{item.date}}</td>
                    <td>{{item.title}}</td>
                    <td class="font-blue">{{addComma(item.income)}}</td>
                    <td class="font-red">{{addComma(item.paid)}}</td>
                </tr>
            </table>
        </div>
        <div class="total-info-area">
            <table class="total-info-table">
                <tr>
                    <td>총 매출</td>
                    <td class="font-blue">{{addComma(data[1].total_income)}}</td>
                </tr>
                <tr>
                    <td>전체 지출</td>
                    <td class="font-red">{{addComma(data[1].total_paid)}}</td>
                </tr>
                <tr>
                    <td>순 이익</td>
                    <td>{{addComma(data[1].total_income - data[1].total_paid)}}</td>
                </tr>
            </table>
        </div>
    </div>
    
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
            data: [],
            selected_cate: 0,
            resize_tl: 0,
            input_date: '',
            input_title: '',
            input_income: '0',
            input_paid: '0',
            result_data: [],
        }
    },
    mounted(){
        setTimeout(function(){
            $('.total-info-area').css({
                'left': ($(window).width()/2)-(1110/2)-249,
            });
        },200)
        

        axios.get('http://localhost:8090/bln-ams-api/bln_history')
        .then(result => {
            this.data = result.data;
            console.log(result);
        })
        .catch(error =>{

        })

        
        

        this.addEvents();

        
    },

    methods: {
        resetModal(){

        },
        handleOk(bvModalEvt){
            bvModalEvt.preventDefault();
            this.handleSubmit();
        },
        handleSubmit(){
            axios.get('http://localhost:8090/bln-ams-api/bln_history_add', {
                params: {
                    date: this.input_date,
                    title: this.input_title,
                    income: this.input_income,
                    paid: this.input_paid,
                }
            })
            .then(result => {
                this.data = result.data;
                console.log(result);
            })
            .catch(error =>{

            })

            this.$nextTick(() => {
                this.$bvModal.hide('modal-input')
            })
        },
        addEvents(){
            $(window).on('resize', function(){
                $('.total-info-area').css({
                    'left': ($(window).width()/2)-(1110/2)-249,
                });
            })
        },

        addComma(num){
            var regexp = /\B(?=(\d{3})+(?!\d))/g;
            return num.toString().replace(regexp, ',');
        },

    },
    props: {
        msg: String
    }
}
</script>

<style>
.container-main{
    padding-top: 30px;
}

.main-table-wrapper {
    position: relative;
    text-align: -webkit-center;
    z-index: 100;
}

.main-table {
    width: 1110px;
    background-color: white;
    /* margin-top: 50px; */
}

.search-area {
    width: 100%;
}

.search-table td {
    padding: 10px;
}

.start-date-form {
    width: 300px;
}

.end-date-form {
    width: 300px;
}

.radio-cate {
    float: left;
    margin-right: 20px;
}

.btn-wrap {
    width: 100%;
    float:right;
}

.btn {
    margin-left:10px;
}

.input-table {
    border-top: 1px solid #CCCCCC;
    border-collapse: collapse;
}

.input-table td {
    text-align: center;
    padding: 10px;
    padding-bottom: 15px;
    border-top: 1px solid #CCCCCC;
}

.date-input {
    width: 130px;
}

.total-info-area {
    position:fixed;
    left:0px;
    top: 206px;
    width: 250px;
    height: 140px;
    background-color: white;
    z-index: 100;
    border: 1px solid #dddddd;
}

.total-info-table td{
    padding: 10px;
    text-align: left;
}
</style>