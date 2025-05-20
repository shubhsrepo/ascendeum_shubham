# ascendeum_shubham


with
   cte1
   as
   (
       select *
       from ascen
   ),
   cte2
   as
   (
       select resource_id, date, weekday, sum(datediff(SECOND, start_time,end_time))  as workingSeconds,
           datepart(ww,created_time) as weeknumber
       from cte1
       group by resource_id,date,weekday,created_time
   )
SELECT resource_id, weeknumber, avg(workingSeconds) as totalwork_in_sec,
   avg(workingSeconds)/60 as totalwork_in_mins
from cte2
group by resource_id,weeknumber
order by resource_id, weeknumber
