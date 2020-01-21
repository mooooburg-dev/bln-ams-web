<template>
    <div class="conatiner-main">
        <div>
            <!-- <h2>B-AMS</h2> -->
        </div>
        <div class="search-area">
            <table class="search-table" style="width:100%; height:80px;">
                <colgroup>
                    <col width=30%>
                    <col width=54%>
                    <col width=16%>
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
                                        <td>column1</td>
                                        <td>column2</td>
                                        <td>column3</td>
                                        <td>column4</td>
                                    </tr>
                                    <tr>
                                        <td>1</td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                    </tr>
                                    <tr>
                                        <td>2</td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                    </tr>
                                    <tr>
                                        <td>3</td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                    </tr>
                                    <tr>
                                        <td>4</td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                    </tr>
                                    <tr>
                                        <td>5</td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                        <td><input type="Start Date" class="form-control" id="Start Data"></td>
                                    </tr>
                                </table>
                            </b-modal>
                        </div>
                    </td>
                </tr>
            </table>
            
        </div>
        <div class="total-info-area">
            <table class="total-info-table">
                <tr>
                    <td>Info1</td>
                    <td>0,000,000</td>
                </tr>
                <tr>
                    <td>Info2</td>
                    <td>0,000,000</td>
                </tr>
            </table>
        </div>
        <div class="main-table-wrapper">
            <table class="table-bordered main-table" border="1">
                <tr>
                    <td>column1</td>
                    <td>column2</td>
                    <td>column3</td>
                    <td>column4</td>
                    <td>column5</td>
                </tr>
                <tr v-for="(item, item_idx) of test_obj">
                    <td>{{item.data1}}</td>
                    <td></td>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
            </table>
        </div>
        
    </div>
    
</template>

<script>
export default {
    data(){
        return{
            test_obj: [
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
                {'data1':'2020.01.20', 'data2':'data2', 'data3':'data3', 'data4':'data4', 'data5':'data5'},
            ],

            selected_cate: 0,
            resize_tl: 0,
        }
    },
    mounted(){
        this.resize_tl = ($(window).width()/2)-(1110/2)-249;
        $('.total-info-area').css({
            'left': this.resize_tl,
        });
        
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
        }
    },
    props: {
        msg: String
    }
}
</script>

<style>
.wrapper{
    /* width: 100%; */
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
.main-table tr{
    text-align: center;
    height: 50px;
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
    top: 150px;
    width: 250px;
    height: 100px;
    background-color: white;
    z-index: 100;
    border: 1px solid #dddddd;
}

.total-info-table td{
    padding: 5px;
}
</style>