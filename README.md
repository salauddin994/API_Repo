# API_Repo

//Post call for signUp:
//pre request:

//Create student dynamic test data 
pm.environment.set("firstName",pm.variables.replaceIn('{{$randomFirstName}}'));
pm.environment.set("lastName",pm.variables.replaceIn('{{$randomLastName}}'));
pm.environment.set("email",pm.variables.replaceIn('{{$randomEmail}}'));
pm.environment.set("dob_month",_.random(1,12));
pm.environment.set("dob_day",_.random(1,31));
pm.environment.set("dob_year",_.random(1935,2013));
const genderList =["male","female"];
const pickGender =Math.floor(Math.random()*genderList.length);
pm.environment.set("gender",genderList[pickGender]);


//Body:

{
    "firstName" : "{{firstName}}",
    "lastName" : "{{lastName}}",
    "email"     : "{{email}}",
    "password"  : "123456",
    "confirmPassword"  : "123456",
    "dob"       : {
        "year"      : {{dob_year}},
        "month"     : {{dob_month}},
        "day"       : {{dob_day}}
    },
    "gender"    : "{{gender}}",
    "agree"     : true
}


//test:

const responsebody =pm.response.json();
pm.environment.set("ID",pm.variables.replaceIn(responsebody.id));

pm.test("asserting with success message and status code",function(){
pm.response.to.have.status(201);
pm.expect(responsebody.success).to.eql(true);
pm.expect(responsebody.message).to.eql("Registration Success");



})



//login post call 

//Body:

const responsebody =pm.response.json();
pm.environment.set("ID",pm.variables.replaceIn(responsebody.id));

pm.test("asserting with success message and status code",function(){
pm.response.to.have.status(201);
pm.expect(responsebody.success).to.eql(true);
pm.expect(responsebody.message).to.eql("Registration Success");



})


//Test:

const responsebody = pm.response.json();
pm.environment.set("authorizationToken",pm.variables.replaceIn(responsebody.token));

pm.test("asserting with success message and status code",function(){
pm.response.to.have.status(200);
pm.expect(responsebody.success).to.eql(true);
pm.expect(responsebody.message).to.eql("Login Success");

})





