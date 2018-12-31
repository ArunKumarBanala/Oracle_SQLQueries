# Oracle_SQLQueries



create table department (deptno number(6), deptname varchar2(100), location varchar2(100), constraint pk_dept primary key (deptno));

insert into department values(1, 'Research', 'hyderanbad');

insert into department values(2, 'Programming', 'Delhi');

insert into department values(3, 'Social', 'Mumbai');

insert into department values(4, 'Software', 'Klcutta');

insert into department values(5, 'Hardware', 'Chennai');

select * from department;

select * from department where deptno=2 and deptno=1;

select dept.deptno,dept.deptname from department dept  where deptno in (2,1);

select * from department where deptname = 'Research';

select * from department where deptname in( 'Research','Programming');

select * from department where deptname like '%ware%';
select * from department where deptno=4 and deptname ='Software';

select * from department where deptno=4 or deptname ='Hardware';

select * from department where deptno=1 or deptname like '%r%';

select count(*) from department;

select * from department;

update department set location='Hyderabad' where deptname like '%ware' ;

update department set location='Chennai' where deptname = 'Software'  ;

delete from department;

delete from department where deptno=2;



-- =============================================================================================


create table employee (empno number(6), empname varchar2(100), job varchar2(100), joindate date, salary number(6,2),deptno number(6),
constraint pk_emp primary key (empno),
constraint fk_deptno foreign key (deptno) references department (deptno)
);

select * from employee;

insert into employee values(1, 'Arun', 'Programmer', to_date('19-12-2018', 'dd-mm-yyyy'), 1000,2);

insert into employee values(2, 'Venkat', 'IT', to_date('12-11-2018', 'dd-mm-yyyy'), 700,5);

insert into employee values(3, 'Surya', 'Admin', to_date('17-11-2015', 'dd-mm-yyyy'), 300,2);

insert into employee values(4, 'Arjun', 'IT', to_date('12-11-2010', 'dd-mm-yyyy'), 700,5);

insert into employee values(5, 'Sunny', 'Financial', to_date('12-01-2013', 'dd-mm-yyyy'), 600,1);


select emp.empno, emp.empname,emp.salary,dept.deptno, dept.deptname from employee emp, department dept where dept.deptno=1;

select emp.empno, emp.empname,emp.salary,dept.deptno, dept.deptname from employee emp left join department dept on emp.deptno=dept.deptno ;

select dept.deptno, dept.deptname,emp.empno from department dept left join  employee emp on dept.deptno=emp.deptno ;

select dept.deptno, dept.deptname,emp.empno from department dept inner join  employee emp on dept.deptno=emp.deptno ;

select * from employee;

select * from department;
-- ===========================================================================================================

select emp.empno,emp.empname,dept.deptno,dept.deptname from employee emp left join department dept on emp.deptno=dept.deptno;

select emp.empno,emp.empname,dept.deptno,dept.deptname from employee emp right join department dept on emp.deptno=dept.deptno;

select emp.empno,emp.empname,dept.deptno,dept.deptname from employee emp left join department dept on emp.deptno=dept.deptno;

select sum(salary) from employee;

select sum(salary) from employee where deptno=5;

select * from employee;

select * from employee order by salary asc;
select * from employee order by salary desc;

select max(salary) from employee;

select * from employee where salary = (select max(salary) from employee);

select sum(emp.salary),dept.deptno,dept.deptname from employee emp inner join department dept on emp.deptno=dept.deptno group by dept.deptno,dept.deptname;

select * from employee where deptno not in (1,2);

select * from employee where deptno is not null;

select * from employee where deptno is null;

select * from employee where joindate='19-Dec-2018';

select sum(emp.salary),deptno from employee emp group by emp.deptno;

select emp.empname,e,p.empno,loan.loanno,loan.loanname,loan.amloun,dept.deptno,dept.deptnamet from employee emp left join emploan loan on emp.empno=loan.empno left join  department dept on dept.deptno=emp.deptno;

loanis,
loannane,
amount
empno





-- =========================================================================================================================


create table classes (classId number(10), className varchar2(50), trainerId number(10), trainerName varchar2(50), studentsIds varchar2(100), createdOn date default sysdate, createdBy varchar2(50), constraint pk_classId primary key (classId));

select * from classes;

CREATE SEQUENCE classes_seq START WITH 1;

CREATE OR REPLACE TRIGGER classes_bir 
BEFORE INSERT ON classes 
FOR EACH ROW

BEGIN
  SELECT classes_seq.NEXTVAL
  INTO   :new.classId
  FROM   dual;
END;

alter table classes AUTO_INCREMENT=1;

-- ==================================================================================


create table post (id number(6), created_at TIMESTAMP, updated_at TIMESTAMP, content varchar2(100), description varchar2(250), title varchar2(100), constraint pk_postid primary key (id));

select * from post;
desc post;

create SEQUENCE post_seq start with 1;

create or replace trigger post_dir
before insert on post
for each row

begin 
select post_seq.nextval
into :new.id
from dual;
end;

drop table post;


create table comments (id number(6), created_at TIMESTAMP, updated_at TIMESTAMP, text varchar2(100), post_id number(6), constraint pk_commentid primary key (id), constraint fk_postid foreign key(post_id) references post (id));


create sequence comments_seq start with 1;

create or replace trigger comments_dir
before insert on comments
for each row
begin
select comments_seq.nextval
into :new.id
from dual;
end;

select * from comments;

drop trigger comments_dir;

drop sequence comments_seq;

drop table comments;

-- =====================================================================================================================



