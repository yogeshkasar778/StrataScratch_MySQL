# StrataScratch MySQL Question and Answer - 

## `Difficulty Level - Easy`

 ### Q.1 Count the number of user events performed by MacBookPro users. Output the result along with the event name. Sort the result based on the event count in the descending order.
   `Company Name - Apple`
  
  playbook_events-
  
    user_id: int
    occurred_at: datetime
    event_type: varchar
    event_name: varchar
    location: varchar
    device: varchar
    
 ###  Solution - 
    
    select distinct count(*) as event_count, event_name
    from playbook_events
    where device = 'macbook pro'
    group by event_name
    order by event_count;

 ### Q.2 Find the average number of bathrooms and bedrooms for each city's property type. Output the reasult along with the city name and property type.
   `Company Name - Airbnb`
  
airbnb_search_details

    Unnamed: 0: int
    id: int
    price: float
    property_type: varchar
    room_type: varchar
    amenities: varchar
    accommodates: int
    bathrooms: int
    bed_type: varchar
    cancellation_policy: varchar
    cleaning_fee: bool
    city: varchar
    host_identity_verified: varchar
    host_response_rate: varchar
    host_since: datetime
    neighbourhood: varchar
    number_of_reviews: int
    review_scores_rating: float
    zipcode: int
    bedrooms: int
    beds: int

 ###  Solution - 
    
    select city, property_type, avg(bathrooms) as avg_bathrooms, avg(bedrooms) as avg_bedrooms
    from airbnb_search_details
    group by city,property_type
    order by city,property_type desc;

 ### Q.3 Find the most profitable company from the financial sector. Output the result along with the continent.
   `Company Name - Forbes`
  
  forbes_global_2010_2014
 
    company: varchar
    sector: varchar
    industry: varchar
    continent: varchar
    country: varchar
    marketvalue: float
    sales: float
    profits: float
    assets: float
    rank: int
    forbeswebpage: varchar
    
 ###  Solution - 
    
    select continent, company
    from forbes_global_2010_2014
    where sector = 'Financials'
    group by continent
    order by continent asc
    limit 1;
    
  ### Q.4 Find the activity date and the pe_description of facilities with the name 'STREET CHURROS' and with a score of less than 95 points.
   `Company Name - City of Los Angeles`
  
  los_angeles_restaurant_health_inspections

    serial_number: varchar
    activity_date: datetime
    facility_name: varchar
    score: int
    grade: varchar
    service_code: int
    service_description: varchar
    employee_id: varchar
    facility_address: varchar
    facility_city: varchar
    facility_id: varchar
    facility_state: varchar
    facility_zip: varchar
    owner_id: varchar
    owner_name: varchar
    pe_description: varchar
    program_element_pe: int
    program_name: varchar
    program_status: varchar
    record_id: varchar
    
 ###  Solution - 
    
    select activity_date, pe_description
    from los_angeles_restaurant_health_inspections
    where facility_name = 'STREET CHURROS' and score < 95;
    
 ### Q.5 Find the details of each customer regardless of the whether the customer made an order Output the customer's first name, last name and the city along with the order details You may have duplicate rows in your results due to a customer ordering several of the same items. Sort records based on the customer's first name and the order details in asending orders.
   `Company Name - Apple, Amazon`
  
  customers-
  
    id: int
    first_name: varchar
    last_name: varchar
    city: varchar
    address: varchar
    phone_number: varchar
    
  orders-
  
    id: int
    cust_id: int
    order_date: datetime
    order_details: varchar
    total_order_cost: int  
    
    
 ###  Solution - 
    
    select first_name, last_name, city, order_details
    from customers
    left join orders on customers.id = orders.cust_id
    order by first_name, order_details desc;
    
 ### Q.6 Find the order details made by Jill and Eva. Consider the Jill and Eva as first names of customers. Output the order date, details and cost along with the first name. Order records based on the customer id in asending order. 
   `Company Name - Amazon, Shopify`
  
  customers-
  
    id: int
    first_name: varchar
    last_name: varchar
    city: varchar
    address: varchar
    phone_number: varchar
    
   orders-
  
    id: int
    cust_id: int
    order_date: datetime
    order_details: varchar
    total_order_cost: int
    
 ###  Solution - 
    
    select c.first_name, o.order_date, o.order_details, o.total_order_cost
    from customers as c
    join orders as o on c.id = o.cust_id
    where c.first_name in ("Jill", "Eva")
    order by c.id;
    
 ### Q.7 Compare's of each employees salary with the average salary of the corresponding department. Output the department, first name, and salary of employees along with the average salary of that department.
   `Company Name - Glassdoor, Salesforce`
  
  employee-
  
    id: int
    first_name: varchar
    last_name: varchar
    age: int
    sex: varchar
    employee_title: varchar
    department: varchar
    salary: int
    target: int
    bonus: int
    email: varchar
    city: varchar
    address: varchar
    manager_id: int
    
 ###  Solution - 
    
    select department, first_name, salary, avg(salary) over (partition by department) as avg_salary
    from employee;
    
 ### Q.8 Find libraries who haven't provided the email address in circulation year 2016 but their notice preference definition is set to email. Output the library code.
   `Company Name - City of San Francisco`
  
  library_usage -
  
    patron_type_code: int
    patron_type_definition: varchar
    total_checkouts: int
    total_renewals: int
    age_range: varchar
    home_library_code: varchar
    home_library_definition: varchar
    circulation_active_month: varchar
    circulation_active_year: float
    notice_preference_code: varchar
    notice_preference_definition: varchar
    provided_email_address: bool
    year_patron_registered: int
    outside_of_county: bool
    supervisor_district: float
    
 ###  Solution - 
    
    select home_library_code
    from employee
    where provided_email_address = 0 and circulation_active_year = 2016 
          and notice_preference_definition = 'email';    
    
 ### Q.9 Fine the base pay for Police Captains. Output the employee name along with the corresponding base pay. 
   `Company Name - City of San Francisco`
  
  sf_public_salaries -
  
    id: int
    employeename: varchar
    jobtitle: varchar
    basepay: float
    overtimepay: float
    otherpay: float
    benefits: float
    totalpay: float
    totalpaybenefits: float
    year: int
    notes: datetime
    agency: varchar
    status: varchar
    
 ###  Solution - 
    
    select employeename, basepay
    from sf_public_salaries
    where jobtitle = 'CAPTAIN III (POLICE DEPARTMENT)';    
        
 ### Q.10 Find how many times each artist appeared on the Spotify ranking list. Output the artist name along with the corresponding number of occurrences. Order records by the number of occurrences in descending order.
   `Company Name - Spotify`
  
  spotify_worldwide_daily_song_ranking -
  
    id: int
    position: int
    trackname: varchar
    artist: varchar
    streams: int
    url: varchar
    date: datetime
    region: varchar
    
 ###  Solution - 
    
    select artist, count(artist) as number_of_occurrences
    from  spotify_worldwide_daily_song_ranking 
    group by artist
    order by number_of_occurrences desc;    
            
 ### Q.11 Find all Lyft drivers who earn eithers equal to or less than 30K USD or equal to more than 70K USD. Output all details related to retrived records.
   `Company Name - Lyft`
  
  lyft_drivers -
  
    index: int
    start_date: datetime
    end_date: datetime
    yearly_salary: int
    
 ###  Solution - 
    
    select *
    from  lyft_drivers 
    where yearly_salary <= 30000 or yearly_salary >= 70000;        
    
 ### Q.12 Meta/Facebook has developed a new programing language called Hack. To measure the popularity of Hack they ran a survey with their employees. The survey included data on previous programing familiarity as well as the number of years of experience, age, gender and most importantly satisfaction with Hack. Due to an error location data was not collected, but your supervisor demands a report showing average popularity of Hack by office location. Luckily the user IDs of employees completing the surveys were stored. Based on the above, find the average popularity of the Hack per office location.Output the location along with the average popularity.
   `Company Name - Meta/Facebook`
  
  facebook_employees -
  
    id: int
    location: varchar
    age: int
    gender: varchar
    is_senior: bool
    
  facebook_hack_survey -
  
    employee_id: int
    age: int
    gender: varchar
    popularity: int  
    
 ###  Solution - 
    
    select fe.location, avg(popularity) as avg_popularity
    from  facebook_employees as fe 
    left join facebook_hack_survey as fh
    group by fe.location;            
    
 ### Q.13 Find all post which were reacted to with a heart. For such posts output all columns from facebook posts table.
   `Company Name - Meta/Facebook`
  
  facebook_reactions -
  
    poster: int
    friend: int
    reaction: varchar
    date_day: int
    post_id: int
    
   facebook_posts -
  
    post_id: int
    poster: int
    post_text: varchar
    post_keywords: varchar
    post_date: datetime

 ###  Solution - 
    
    select fp.*
    from  facebook_reactions as fr
    join facebook_posts as fp on fr.post_id = fp.post_id
    where reaction = 'heart';     
    
 ### Q.14 Count the number of movies that Abigail Breslin was nominated for an oscar.
 
   `Company Name -  Google, Netflix`
  
  oscar_nominees -
  
    year: int
    category: varchar
    nominee: varchar
    movie: varchar
    winner: bool
    id: int
    

 ###  Solution - 
    
    select movie, count(movie) as count_of_movie
    from  oscar_nominees 
    where nominee = 'Abigail Breslin'
    group by movie;         
    
 ### Q.15 Find the last time each bike was in use. Output both the bike number and the date-timestamp of the bike's last use (i.e., the date-time the bike was returned). Order the results by bikes that were most recently used.
 
   `Company Name -  Lyft, DoorDash`
  
  dc_bikeshare_q1_2012 -
  
    duration: varchar
    duration_seconds: int
    start_time: datetime
    start_station: varchar
    start_terminal: int
    end_time: datetime
    end_station: varchar
    end_terminal: int
    bike_number: varchar
    rider_type: varchar
    id: int
    

 ###  Solution - 
    
    select bike_number, max(end_time) as last_time_use
    from  dc_bikeshare_q1_2012
    group by bike_number
    order by end_time desc;             
    
 ### Q.16 We have a table with employees and their salaries, however, some of the records are old and contain outdated salary information. Find the current salary of each employee assuming that salaries increase each year. Output their id, first name, last name, department ID, and current salary. Order your list by employee ID in ascending order.
 
   `Company Name -  Microsoft`
  
  ms_employee_salary -
  
    id: int
    first_name: varchar
    last_name: varchar
    salary: int
    department_id: int
    

 ###  Solution - 
    
    select 
          id,
          first_name,
          last_name,
          department_id,
          max(salary) as current_salary
    from  ms_employee_salary
    group by id,
             first_name,
             last_name,
             department_id
    order by id asc;           
    
   ### Q.17 Write a query that calculates the difference between the highest salaries found in the marketing and engineering departments. Output just the absolute difference in salaries.
 
   `Company Name -  LinkedIn, Dropbox`
  
  db_employee -
  
    id: int
    first_name: varchar
    last_name: varchar
    salary: int
    department_id: int
    
  db_dept -
  
    id: int
    department: varchar
    
 ###  Solution - 
    
    select abs(max(a.salary) - max(b.salary)) as sal_diff
    from db_employee a, db_employee b
    where a.department_id = 4 and b.department_id = 1; 
    
### Q.18 Write a query that returns the number of unique users per client per month.
   `Company Name -  Apple, Dell, Microsoft`
  
  fact_events -
  
    id: int
    time_id: datetime
    user_id: varchar
    customer_id: varchar
    client_id: varchar
    event_type: varchar
    event_id: int
    
 ###  Solution - 
    
    select client_id, extract(month from time_id) as month,
    count(distinct user_id) as user_num
    from fact_events
    group by client_id, month;    

### Q.19 Write a query that will calculate the number of shipments per month. The unique key for one shipment is a combination of shipment_id and sub_id. Output the year_month in format YYYY-MM and the number of shipments in that month.
   `Company Name -  Amazon`
  
  amazon_shipment -
  
    shipment_id: int
    sub_id: int
    weight: int
    shipment_date: datetime
    
 ###  Solution - 
    
    select to_char(shipment_date, 'YYYY-MM') as year_month,
    count(concat(shipment_id,sub_id)) as user_num
    from amazon_shipment
    group by year_month;    
        
## `Difficulty Level - Medium`

   ### Q.18 What were the top 10 ranked songs in 2010? Output the rank, group name, and song name but do not show the same song twice. Sort the result based on the year_rank in ascending order.
 
   `Company Name -  Spotify`
  
  billboard_top_100_year_end -
  
    year: int
    year_rank: int
    group_name: varchar
    artist: varchar
    song_name: varchar
    id: int

    
 ###  Solution - 
    
    select year_rank, group_name, song_name
    from billboard_top_100_year_end 
    where year = '2010'
    order by year_rank asc
    limit 10;  

 ### Q.19 Classify each business as either a restaurant, cafe, school, or other.
•	A restaurant should have the word 'restaurant' in the business name.
•	A cafe should have either 'cafe', 'café', or 'coffee' in the business name.
•	A school should have the word 'school' in the business name.
•	All other businesses should be classified as 'other'.

Output the business name and their classification.
 
   `Company Name -  City of San Francisco`
  
  sf_restaurant_health_violations -
  
    business_id: int
    business_name: varchar
    business_address: varchar
    business_city: varchar
    business_state: varchar
    business_postal_code: float
    business_latitude: float
    business_longitude: float
    business_location: varchar
    business_phone_number: float
    inspection_id: varchar
    inspection_date: datetime
    inspection_score: float
    inspection_type: varchar
    violation_id: varchar
    violation_description: varchar
    risk_category: varchar

    
 ###  Solution - 
    
    select 
       business_name,
       case
            when business_name like '%restaurant%' then 'restaurant'
            when business_name like '%school%' then 'school'
            when business_name like '%café%' then 'cafe'
            when business_name like '%coffee%' then 'cafe'
            when business_name like '%cafe%' then 'cafe'
            else 'other' end as classification
    from sf_restaurant_health_violations
    group by binary business_name;  
    
### Q.20 You're given a dataset of health inspections. Count the number of violation in an inspection in 'Roxanne Cafe' for each year. If an inspection resulted in a violation, there will be a value in the 'violation_id' column. Output the number of violations by year in ascending order.
 
   `Company Name -  City of San Francisco`
  
  sf_restaurant_health_violations -
  
    business_id: int
    business_name: varchar
    business_address: varchar
    business_city: varchar
    business_state: varchar
    business_postal_code: float
    business_latitude: float
    business_longitude: float
    business_location: varchar
    business_phone_number: float
    inspection_id: varchar
    inspection_date: datetime
    inspection_score: float
    inspection_type: varchar
    violation_id: varchar
    violation_description: varchar
    risk_category: varchar
    
 ###  Solution - 
    
    select extract(year from inspection_date) as year, count(violation_id) as n_inspections
    from sf_restaurant_health_violations 
    where business_name = 'Roxanne Cafe'
    group by year
    order by n_inspections asc;   
    
### Q.21 Find the rate of processed tickets for each type.
 
   `Company Name -  Meta/Facebook`
  
  facebook_complaints -
  
    complaint_id: int
    type: int
    processed: bool
    
 ###  Solution - 
    
    select type, avg(processed) as processed_rate
    from facebook_complaints
    group by type;    

### Q.22 Calculate the total revenue from each customer in March 2019. Include only customers who were active in March 2019.


Output the revenue along with the customer id and sort the results based on the revenue in descending order.
 
   `Company Name -  Amazon, Meta/Facebook`
  
  orders -
  
    id: int
    cust_id: int
    order_date: datetime
    order_details: varchar
    total_order_cost: int
    
 ###  Solution - 
    
    select cust_id, sum(total_order_cost) as revenue
    from orders
    where date(order_date) between '2019-03-01' and '2019-03-31'
    group by cust_id
    order by revenue desc;    

### Q.23 Find employees who are earning more than their managers. Output the employee's first name along with the corresponding salary.

   `Company Name -  Walmart, Best Buy, Dropbox`
  
  employee -
  
    id: int
    first_name: varchar
    last_name: varchar
    age: int
    sex: varchar
    employee_title: varchar
    department: varchar
    salary: int
    target: int
    bonus: int
    email: varchar
    city: varchar
    address: varchar
    manager_id: int
    
 ###  Solution - 
    
    select e.first_name, e.salary
    from employee e
    join employee em on e.manager_id = em.id
    where e.salary > em.salary;  

### Q.24 Find the employee with the highest salary per department. Output the department name, employee's first name along with the corresponding salary.

   `Company Name -  Twitter, Asana`
  
  employee -
  
    id: int
    first_name: varchar
    last_name: varchar
    age: int
    sex: varchar
    employee_title: varchar
    department: varchar
    salary: int
    target: int
    bonus: int
    email: varchar
    city: varchar
    address: varchar
    manager_id: int
    
 ###  Solution - 
    
    select department, first_name, salary
    from employee
    where salary in (select max(salary) from employee group by department);  

### Q.25 Find the highest target achieved by the employee or employees who works under the manager id 13. Output the first name of the employee and target achieved. The solution should show the highest target achieved under manager_id=13 and which employee(s) achieved it.

   `Company Name -  Saleforce`
  
  salesforce_employees -
  
    id: int
    first_name: varchar
    last_name: varchar
    age: int
    sex: varchar
    employee_title: varchar
    department: varchar
    salary: int
    target: int
    bonus: int
    email: varchar
    city: varchar
    address: varchar
    manager_id: int
    
 ###  Solution - 
    
    with target_achived as
    (select first_name, target, rank() over(order by target desc) as rnk
    from salesforce_employees
    where manager_id = 13)
    
    select first_name, target
    from target_achived
    where rnk = 1;  

### Q.26 Find the customer with the highest daily total order cost between 2019-02-01 to 2019-05-01. If customer had more than one order on a certain day, sum the order costs on daily basis. Output customer's first name, total cost of their items, and the date.

For simplicity, you can assume that every first name in the dataset is unique.

   `Company Name -  Amazon, Shofify`
  
  customers -
  
    id: int
    first_name: varchar
    last_name: varchar
    city: varchar
    address: varchar
    phone_number: varchar

  orders -
  
    id: int
    cust_id: int
    order_date: datetime
    order_details: varchar
    total_order_cost: int
    
 ###  Solution - 
    
    select customers.id, order_date, first_name, sum(total_order_cost) as tl_cost
    from customers
    right join orders on customers.id = orders.cust_id
    where order_date between '2019-05-01' and '2019-05-01' 
    group by customer.id, order_date
    order by tl_cost desc
    limit 1;  

### Q.27 Find the Olympics with the highest number of athletes. The Olympics game is a combination of the year and the season, and is found in the 'games' column. Output the Olympics along with the corresponding number of athletes.

   `Company Name -  ESPN`
  
  olympics_athletes_events -
  
    id: int
    name: varchar
    sex: varchar
    age: float
    height: float
    weight: datetime
    team: varchar
    noc: varchar
    games: varchar
    year: int
    season: varchar
    city: varchar
    sport: varchar
    event: varchar
    medal: varchar
    
 ###  Solution - 
    
    select games, count(distinct id) as athletes
    from olympics_athletes_events' 
    group by games
    order by athletes desc
    limit 1;  

### Q.28 Find songs that have ranked in the top position. Output the track name and the number of times it ranked at the top. Sort your records by the number of times the song was in the top position in descending order.

   `Company Name -  Spotify`
  
  spotify_worldwide_daily_song_ranking -
  
    id: int
    position: int
    trackname: varchar
    artist: varchar
    streams: int
    url: varchar
    date: datetime
    region: varchar
    
 ###  Solution - 
    
    select trackname, count(position) as times_top1
    from olympics_athletes_events
    where position = 1
    group by trackname
    order by times_top1 desc;  

### Q.29 Find the top 5 businesses with most reviews. Assume that each row has a unique business_id such that the total reviews for each business is listed on each row. Output the business name along with the total number of reviews and order your results by the total reviews in descending order.

   `Company Name -  Yelp`
  
  yelp_business -
  
    business_id: varchar
    name: varchar
    neighborhood: varchar
    address: varchar
    city: varchar
    state: varchar
    postal_code: varchar
    latitude: float
    longitude: float
    stars: float
    review_count: int
    is_open: int
    categories: varchar
    
 ###  Solution - 
    
    select name, review_count as total_review
    from yelp_business
    order by total_review desc
    limit 5;  

### Q.30 Find all wineries which produce wines by possessing aromas of plum, cherry, rose, or hazelnut. To make it more simple, look only for singular form of the mentioned aromas. HINT: if one of the specified words is just a substring of another word, this should not be a hit, but a miss.

   `Company Name -  Wine Magazine
`
  
  winemag_p1 -
  
    id: int
    country: varchar
    description: varchar
    designation: varchar
    points: int
    price: float
    province: varchar
    region_1: varchar
    region_2: varchar
    variety: varchar
    winery: varchar
    
 ###  Solution - 
    
    select distinct winery
    from winemag_p1
    where lower(description) regexp '(plum|rose|cherry|hazelnut)([^a-z])'; 
    
### Q.31 Find the top business categories based on the total number of reviews. Output the category along with the total number of reviews. Order by total reviews in descending order.

   `Company Name -  yelp`
  
  yelp_business -
  
    business_id: varchar
    name: varchar
    neighborhood: varchar
    address: varchar
    city: varchar
    state: varchar
    postal_code: varchar
    latitude: float
    longitude: float
    stars: float
    review_count: int
    is_open: int
    categories: varchar
    
 ###  Solution - 
    
    WITH RECURSIVE CTE (n) AS (
                  SELECT 1
                  UNION ALL
                  SELECT n+1 FROM CTE WHERE n<12)
    SELECT
       substring_index(substring_index(categories,';',n),';',-1) category,
       SUM(review_count) total
    FROM 
       yelp_business JOIN CTE
    ON 
      n <= char_length(categories) - char_length(replace(categories,';','')) + 1
    GROUP BY 1
    order by total desc;
    
    
    
    
    
    
