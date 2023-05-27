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
    
    
    
    
    
    
    
    
    
    
    
    
