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
    
    
    
    
    
