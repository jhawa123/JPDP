# JPDP
<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html lang="en">
    <head>
        <title>Bootstrap Example</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet"
              href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        <script
        src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script
        src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
        <script
        src="http://login2explore.com/jpdb/resources/js/0.0.3/jpdb-commons.js"></script>

    </head>
    <body>
        <div class="container">
            <h2>Vertical (basic) form</h2>
            <form id="empForm" method="post">
                <div class="form-group">
                    <span><label for="empId">Employee ID:</label> <label id="empIdMsg">
                        </label></span>
                    <input type="text" class="form-control" name="empId" id="empId"
                           placeholder="Enter Employee ID" required>
                </div>
                <div class="form-group">
                    <label for="empName">Employee Name:</label>
                    <input type="text" class="form-control" id="empName"
                           placeholder="Enter Employee Name" name="empName">
                </div>
                <div class="form-group">
                    <label for="empEmail">Email:</label>
                    <input type="email" class="form-control" id="empEmail"
                           placeholder="Enter Employee Email" name="empEmail">
                </div>
                <input type="button" class="btn btn-primary" id="empSave" value="Save"
                       onclick="saveEmployee();">
            </form>
        </div>
        <script>

            function validateAndGetFormData() {
                var empIdVar = $("#empId").val();
                if (empIdVar === "") {
                    alert("Employee ID Required Value");
                    $("#empId").focus();
                    return "";
                }
                var empNameVar = $("#empName").val();
                if (empNameVar === "") {
                    alert("Employee Name is Required Value");
                    $("#empName").focus();
                    return "";
                }
                var empEmailVar = $("#empEmail").val();
                if (empEmailVar === "") {
                    alert("Employee Email is Required Value");
                    $("#empEmail").focus();
                    return "";
                }
                var jsonStrObj = {
                    empId: empIdVar,
                    empName: empNameVar,
                    empEmail: empEmailVar,
                };
                return JSON.stringify(jsonStrObj);
            }

            function resetForm() {
                $("#empId").val("")
                $("#empName").val("");
                $("#empEmail").val("");
                $("#empId").focus();
            }


            function saveEmployee() {
                var jsonStr = validateAndGetFormData();
                if (jsonStr === "") {
                    return;
                }
                var putReqStr = createPUTRequest("90935476|-31948797872834702|90931808",
                        jsonStr, "SAMPLE", "EMP-REL");
                alert(putReqStr);
                jQuery.ajaxSetup({async: false});
                var resultObj = executeCommandAtGivenBaseUrl(putReqStr,
                        "http://api.login2explore.com:5577", "/api/iml");
                alert(JSON.stringify(resultObj));
                jQuery.ajaxSetup({async: true});
                resetForm();
            }


        </script>    
    </body>
</html>
