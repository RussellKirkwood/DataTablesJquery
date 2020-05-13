# DataTablesJquery
Using JQuery Data Tables

full information - https://datatables.net/

The following example shows you how to add "Date From" - "Date To" search to a Data Table

    <link rel="stylesheet" href="https://cdn.datatables.net/1.10.20/css/jquery.dataTables.min.css">
    <script src="https://cdn.datatables.net/1.10.20/js/jquery.dataTables.min.js"></script>
    <script type="text/javascript" src="/Scripts/moment.js"></script>
    <script type="text/javascript" src="/Scripts/bootstrap-datetimepicker.js"></script>
    <link rel="stylesheet" href="/Content/bootstrap-datetimepicker.min.css" />

    <script type="text/javascript">

    $(function () {
        $('#datetimepicker1').datetimepicker({ format: 'MM/DD/YYYY' })
        $('#datetimepicker2').datetimepicker({ format: 'MM/DD/YYYY' })
    });

    </script>
    
    <script>

var tableid = null;
     
        var fromdate = $("#datetimepicker1").find("input").val();
        var todate = $("#datetimepicker2").find("input").val();



$(document).ready(function () {
            tableid = $('#tableid').DataTable({               
                "ajax": "/api/getdata?fromdate=" + fromdate + "&todate=" + todate,
                columns: [
                    { data: "from" },
                    { data: "to" },
                    { data: "somedata" },
                                        {
                        data: "guidid",
                        "render": function (data, type, row, meta) {
                            return '<a target=_blank href="XXX/getdetails/' + data + '">Get Details</a>';
                        }
                    }
                ],
                "oLanguage": {
                    "sSearch": "Quick Search of within this populated data table:"
                },
                "order": []                
            });
        });
</script>
    
    
    
    <script>
        $(document).ready(function () {

            $("#ApplyDateRange").click(function () {               

                fromdate = $('#datetimepicker1').data("DateTimePicker").date().toDate();
                todate = $('#datetimepicker2').data("DateTimePicker").date().toDate();

                var inputemail = $('#InputEmail').val();

                var fromdatedate = (fromdate.getMonth() + 1) + "-" + fromdate.getDate() + "-" + fromdate.getFullYear();
                var todatedate = (todate.getMonth() + 1) + "-" + todate.getDate() + "-" + todate.getFullYear();               
                
                // This populates table with data from API
                tableid.ajax.url('/api/getdata?fromdate=' + fromdatedate + '&todate=' + todatedate + '&inputemail=' + inputemail).load();             

            });
           
        });

    </script>
    
    <body>
    
    
    <div><br /></div>
        <div class="row">
            <div class="col-lg-3">
                <div class='input-group date' id='datetimepicker1'>
                    <input type='text' id="fromdate" class="form-control date-picker" value="@ViewBag.fromdate" name="fromDate" />
                    <span class="input-group-addon form-inline">
                        <span class="glyphicon glyphicon-calendar form-inline"></span>
                    </span>
                </div>
            </div>

            <div class="col-lg-3">
                <div class='input-group date' id='datetimepicker2'>
                    <input type='text' id="todate" class="form-control date-picker" value="@ViewBag.todate" name="toDate" />
                    <span class="input-group-addon form-inline">
                        <span class="glyphicon glyphicon-calendar form-inline"></span>
                    </span>
                </div>
            </div>

            <div class="col-lg-3">
                <div class="form-group">                    
                    <input type="email" class="form-control" id="InputEmail" aria-describedby="emailHelp" placeholder="Enter email">                    
                </div>
            </div>

            <div class="col-lg-3">
                <button class="btn btn-primary dropdown-toggle" type="submit" value="ApplyDateRange" id="ApplyDateRange" name="ApplyDateRange">
                    Search
                </button>
            </div>
            
            <table id="tableid" class="display" />
            <thread>
            <tr>
            <th> from </th>
             <th> to </th>
              <th> somedata </th>
            </tr>
            </thread>
            </table>

</body>
    
