# belajar-postgresql
belajar-postgresql

Belajar PostgreeSql 
Bootcamp: dimas maryanto


-- Perintah Select

SELECT * FROM departments;

SELECT department_id, department_name FROM departments;

-- Pemberian Alias pada Kolom
select 
    -- menggunakan keyword as, untuk mendefinisikan sebagai variable
    department_id as kode_divisi,
    -- tanpa menggunakan keyword as
    department_name nama_department,
    -- menggunakan nama kolom custome
    manager_id as "Kode Manager"  
from departments


-- Operasi Aritmatika di PostgreeSql
select 
    2 + 2 as jumlah,
    2 * 2 as kali,
    2 / 2 as bagi,
    2 ^ 3 as pangkat

-- Contoh menggunakan table
select 
    first_name, 
    salary + 1000 as gaji_plus 
from employees;

-- Salary + 10% dari gaji
select 
	employee_id,
	salary as gaji_bulanan,
	salary * 0.1 as delta,
	salary + (salary * 0.1) as salary_delta
	from employees;

--Concat Penggabungan
Select
	first_name,
	last_name,
	first_name ||' '|| last_name as fullname 
	from employees;

-- Date untuk menghitung masa kerja
SELECT 
	employee_id,
	start_date,
	end_date,
	end_date - start_date as waktu_kerja
from job_history;


-- Distinct digunakan untuk memisahkan data double (unik)

SELECT
	DISTINCT job_id
	FROM employees;
	
SELECT 
	DISTINCT (job_id, salary) as job_by_salary,
	job_id,
	salary
	from employees;


-- Null dan Empty String Handler
select 
    first_name      as name, 
    commission_pct  as komisi_persen, 
    salary          as gaji_sebulan 
from employees;

-- Menggunakan rumus COALESCE untuk mengatasi null dan empty
select 
    first_name                                      as name, 
    COALESCE(commission_pct,0)                      as komisi_persen, 
    salary                                          as gaji_sebulan,
    salary + (salary * COALESCE(commission_pct,0))  as gaji_net
from employees;


-- filter data dengan where klausa
select 
    country_id      as id,
    country_name    as name
from countries
where region_id = 1;


-- equals to (=)
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where employee_id = 100;

-- Not equals (<>) (!=)
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where job_id <> 'IT_PROG';

select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where job_id != 'IT_PROG';

-- more than (>)
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where salary > 12000;

-- bigger equals to (>=)
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where salary >= 24000;

--like (%) (_)
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where last_name like 'A%';

select * 
from jobs 
where job_id like '_T%';

--in
select employee_id, last_name, salary, department_id
from employees 
where department_id in (10, 90,20);

--beetween
select employee_id, first_name, last_name, email, phone_number, job_id, salary, department_id
from employees 
where salary between 4000 and 6000;

--null
select *
	from employees 
	where commission_pct is null;
	
	
--Logical Statement AND, OR, NOT
--AND
select
    employee_id as kode,
    first_name as nama_depan
from employees
where 
    department_id = 90 and 
    manager_id = 100;

--OR
select
    employee_id as kode,
    first_name as nama_depan,
    salary as gaji_bulanan
from employees
where 
    department_id = 90 or 
    salary >= 12000;
	
--NOT
select
    employee_id as kode,
    first_name as nama_depan,
    department_id as divisi,
    salary as gaji_bulanan
from employees
where 
    NOT(department_id = 90);
	
--AND, OR, NOT
select
    employee_id as kode,
    first_name as nama_depan,
    department_id as divisi,
    salary as gaji_bulanan,
    manager_id as manager
from employees
where 
    (department_id = 100 or manager_id = 108) and 
    salary >= 9000 and 
    NOT(first_name = 'Daniel');
	
--ORDER Data a-z, 1-100
--ASC
select
    employee_id as kode,
    first_name as nama_depan,
    salary as gaji
from employees
order by (first_name, salary) asc;

--DESC
select
    employee_id as kode,
    first_name as nama_depan,
    salary as gaji
from employees
order by salary desc;


--LIMIT dan OFFSET
-- limit itu ya seperti bahasa indonesianya yaitu batas maksimum sedangkan offset artinya kita mulai dari baris ke.

select employee_id as kode, first_name as nama
from employees
limit 5 offset 5

--Practice Part 1
--Buatlah query untuk menampilkan seluruh data karyawan dari table employees yang diurutkan berdasarkan email paling terakhir.
select 
	employee_id,
	last_name,
	email,
	salary
from employees 
order by email DESC;

--Buatlah query untuk menampilkan data karyawan yang gajinya lebih besar 3200.00 sampai dengan 12000.00.
select 
	employee_id,
	last_name,
	email,
	salary
	from employees
	where salary between 3200 and 12000;
	
--Buatlah query untuk menampilkan data karyawan yang memiliki huruf A diawal nama depannya
	select * 
	from employees
	where first_name like 'A%';

--Buatlah query untuk menampilkan data karyawan yang memiliki kode karyawan diantaranya 103, 115, 196, 187, 102 dan 100
	select * 
	from employees
	where employee_id in (103,115,196,187,102,100);
	
--Buatlah query untuk menampilkan data karyawan yang nama belakangnya memiliki huruf kedua u	
select * 
	from employees
	where last_name like '_u%';

--Buatlah query untuk menampilkan kode department apa saja yang ada di tabel employees secara unique
select 
	DISTINCT department_id
	from employees;

--Buatlah query untuk menampilkan nama lengkap karyawan, kode jabatan, gaji setahun dari table employees yang kode manager sama dengan 100.
select 
	first_name || ' ' || last_name as nama_lengkap,
	job_id as kode_jabatan,
	salary * 12 as gaji_setahun
	from employees
	where manager_id = '100';

--Buatlah query untuk menampilkan nama belakang, gaji perbulan, kode jabatan dari table employees yang tidak memiliki komisi
select 
	last_name as nama_belakang,
	job_id as kode_jabatan,
	salary as gaji_sebulan,
	manager_id as kode_manager,
	commission_pct as komisi
	from employees
	where commission_pct is null;
	
--Buatlah query untuk menampilkan data karyawan yang bukan dari jabatan IT_PROG dan SH_CLERK.
select 
	last_name as nama_belakang,
	job_id as kode_jabatan,
	salary as gaji_sebulan,
	manager_id as kode_manager,
	commission_pct as komisi
	from employees
	where job_id not in ('IT_PROG','SH_CLERK');


--Text Formatted
select 
    employee_id as kode,
    upper(first_name) as nama_depan_kapital,
    last_name as nama_belakang,
    length(last_name) as jumlah,
    concat(first_name, ' ', last_name) as nama_lengkap,
	to_char(salary,'FM999,999') as gaji_perbulan
from employees
limit 10;

--Number Formatted
select 
    coalesce(commission_pct, 0) as commision_pct,
    salary as gaji,
    mod(2, 4) as sisa_bagi,
    power((salary / 1000), 2) as pangkat,
    sqrt(50) as akar
from employees
limit 10

--Aggregate Function
select
   round(avg(salary), 2) as rata2_gaji,
    count(*) as jml_baris,
    max(salary) as max_salary,
    min(salary) as min_salary,
    sum(salary) as total_salary
from employees;

--Aggregate function with group by
select 
    department_id as kode,
    count(*) as jumlah_karyawan,
    (sum(salary) * 12) as total_salary
from employees
group by kode
order by kode

--multiple group
select 
    department_id as divisi,
    manager_id as manager,
    count(*) as jumlah_karyawan,
    (sum(salary) * 12) as total_salary
from employees
group by divisi, manager
order by divisi

--having
select 
    manager_id,
    count(*) as jumlah_karyawan
from employees
group by manager_id
    having count(*) >= 5
order by manager_id;

--having dan where
select 
    manager_id, 
    count(*) as jumlah_karyawan
from employees
    where salary >= 5000
group by manager_id
    having count(*) >= 5
order by manager_id;


--natural join
select 
    l.location_id kode_lokasi,
    l.city as kota,
    l.state_province as provinsi,
    c.country_name as negara
from 
    locations l natural join countries c;
	
select * from locations;
select * from countries;

--inner join
select 
	emp.employee_id as id,
	dep.department_id as id_departments,
	dep.department_name as name_departments,
	concat(emp.first_name,' ', emp.last_name) as fullname
	from employees emp join departments dep on (emp.employee_id = dep.manager_id) 	
	limit 10;


select 
	emp.employee_id as id,
	dep.department_id as id_departments,
	dep.department_name as name_departments,
	concat(emp.first_name,' ', emp.last_name) as fullname
	from employees emp, departments dep 
	where emp.employee_id = dep.manager_id 	
	limit 10;


--Outer(Left and Right) Join
select
	d.department_id as kode_department,
	d.department_name as name_department,
	d.location_id as department_location_id,
	l.location_id as location_id,
	l.street_address as alamat
	from
		locations l left join departments d on(l.location_id = d.location_id);
		
select
	d.department_id as kode_department,
	d.department_name as name_department,
	d.location_id as department_location_id,
	l.location_id as location_id,
	l.street_address as alamat
	from
		locations l right join departments d on(l.location_id = d.location_id);
		
--Self Join
select 
    e.employee_id as kode_karyawan,
    concat(e.first_name, ' ', e.last_name) as nama_karyawan,
    m.employee_id as kode_manager,
    concat(m.first_name, ' ', m.last_name) as nama_manager
from 
    employees e left join employees m on (e.manager_id = m.employee_id);

--seleksi dengan case when
select
    employee_id as kode_karyawan,
    commission_pct as besar_komisi,
    case    
        when COALESCE(commission_pct, 0) = 0 
            then 'Tidak memiliki komisi'
        else 
            concat('Memiliki komisi sebesar ', commission_pct)
    end as deskripsi
from 
    employees;



select
    employee_id as kode_karyawan,
    commission_pct as besar_komisi,
    case    
        when COALESCE(commission_pct, 0) = 0 
            then 'Tidak memiliki komisi'
		when COALESCE(commission_pct, 0) between 0.2 and 0.4
			then 'Komisi lebih besar dari 0.2 sampai 0.4'
		when COALESCE(commission_pct, 0) < 0.2
			then 'komisi lebih kecil dari 0.2'
        else 
            concat('Memiliki komisi sebesar ', commission_pct)
    end as deskripsi
from 
    employees;

--SubQuery
select
    e.employee_id as nik,
    e.first_name as nama,
    (select j.job_title from jobs j where j.job_id = e.job_id) as jabatan,
    (select j2.min_salary from jobs j2 where j2.job_id = e.job_id) as minimun_salary
from employees e
limit 10;

--SubQuery menggunakan where
select
    e.employee_id as nik,
    e.first_name as nama,
    e.salary as gaji_sebulan
from 
    employees e
where 
    e.salary > (select avg(j.max_salary) from jobs j)
limit 10;

--subquery multiple value
select
    e.employee_id as nik,
    e.first_name as nama,
    e.salary as gaji_sebulan
from 
    employees e
where 
    e.salary in (select j.max_salary from jobs j)
limit 10;

--salary group min salary 5000, max salaary 16000
select 
    round(avg(j.max_salary)) as gaji_rata 
from jobs j 
group by j.job_id
having avg(j.max_salary) < 20000
order by gaji_rata;

-----------
select
    e.employee_id as nik,
    e.first_name as nama,
    e.salary as gaji_sebulan
from 
    employees e
where 
    e.salary > any (
        select 
            round(avg(j.max_salary)) as gaji_rata 
        from jobs j 
        group by j.job_id
        having avg(j.max_salary) < 20000
    );

--Practice Part 2
-- No.1
select
	emp.employee_id as "Kode Karyawan",
	dep.department_name as "Nama Department",
	concat(first_name, ' ',last_name) as "Nama Lengkap",
	to_char(salary, 'FM999,999,999') as "Gaji Sebulan",
	case
		when coalesce(commission_pct, 0) = 0 
			then 'Tidak punya komisi'
		else
			to_char(coalesce(commission_pct, 0) * salary, 'FM999,999,999')
	end as "Mendappatkan Komisi",
	salary + (coalesce(commission_pct, 0) * salary) as gaji_terima
from
	employees emp join departments dep on(emp.department_id = dep.department_id);

--No. 2
select
	emp.employee_id as employee_id,
	concat(emp.first_name, ' ', emp.last_name) as employee_name,
	case 
		when man.employee_id is null
			then 'Saya tidak memiliki manager'
		else
			to_char(man.employee_id, 'FM999') 
		end as manager_id,
	concat(man.first_name,' ',man.last_name) as manager_name,
	job.job_title as "Nama Jabatan"
from
	employees emp left join employees man on (emp.manager_id = man.employee_id)
	join jobs job on(emp.job_id = job.job_id)
order by manager_name, employee_name ;

--No.3
select
	dep.department_id as dep_id,
	dep.department_name as dep_name,
	sum(emp.salary) as total_gaji
from
	employees emp join departments dep on(dep.department_id = emp.department_id)
group by dep_id, dep_name
order by total_gaji desc;

--No.4
select
	salary * 12 as gaji_setahun,
	count(employee_id) as jumlah_karyawan
from
	employees emp
	where commission_pct is not null
	group by gaji_setahun
	order by gaji_setahun desc;

--No. 5
select 
	emp.employee_id as kode_karyawan,
	concat(first_name,' ',last_name) as nama_lengkap,
	to_char(salary, 'FM999,999,999') as gaji_karyawan,
	job.job_title as jabatan,
	emp.email as email
from
	employees emp join jobs job on(emp.job_id = job.job_id) 
where emp.salary > (select max(emp1.salary) from employees emp1
				   where emp1.job_id = 'IT_PROG');


--Data Manipulation Language
--insert
insert into regions (region_id,region_name) values (5,'Asia Tenggara');
select * from regions;

--update
update regions SET region_name = 'Oceania' where region_id = 5;

--delete
delete from regions where region_id = 5;

--Transaction Control Language (TCL)
--Begin Rollback
begin
insert into regions (region_id,region_name) values (5,'Asia Tenggara'),(6,'Oceania');
delete from regions where region_id = 6;
select * from regions;
rollback

--Begin Commit
begin
insert into regions (region_id,region_name) values (5,'Asia Tenggara'),(6,'Oceania')
commit
select * from regions;


-- Data Definition Language(DDL)
--Create Table
CREATE TABLE example_table(
	kode serial primary key,
	nama_depan character varying(50) not null,
	nama_belakang character varying(60),
	tanggal_lahir date not null default '1999-01-01',
	saldo decimal default 0,
	aktif boolean default false,
	created_datetime timestamp not null default now()
);

select * from example_table;
--DROP Table
drop table example_table;
--Alter Table
alter table example_table ADD COLUMN bunga integer default 0;
--Truncate Table
--RENAME TAble

--Membuat User Postgreesql DDL
--Create
create user example with superuser login password 'admin';
--DROPM
--Alter
--Grant
--Revoke
