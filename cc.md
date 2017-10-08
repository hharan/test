
# Canine Company API requirements for communicating with the Datacenter.

### All API calls start with a base URL
something like
<pre class="base">
https://www.caninecompany.com/api/v1/
</pre>

### Path

For this documentation, we will assume every request begins with the above path.

### Format

All calls are returned in **JSON** or **XML**

### Status Codes

- **200** Successful GET and PUT.
- **201** Successful POST.
- **202** Successful Provision queued.
- **204** Successful DELETE
- **401** Unauthenticated.
- **403** Forbidden.
- **409** Unsuccessful POST, PUT, or DELETE (Will return an errors object)

# Users

## POST /login

Service used to authenticate the user in the app. 

#### Parameters

###### email
###### password

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "email":"text@example.com","password":"hash/encrypted value" https://www.caninecompany.com/api/v1/login


#### response
    <xml>
        <status>success</status>
        <user_id>xxxxxxxx</user_id>
        <token>auth token</token>
    </xml>

auth token will be passed in the authentication header (HMAC) for all other calls.

## GET /user/:id

Get a user detail using user id. 


#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/user/<user_id>

#### response
    <xml>
        <status>success</status>
        <user_name>...</user_name>
        <address>...</address>
        <email>...</email>
        <phone>...</phone>
    </xml>

## PUT /user/:id

Modified user data

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" -X PUT https://www.caninecompany.com/api/v1/user/<user_id>

#### response
    <xml>
        <status>success</status>
        <user_name>...</user_name>
        <address>...</address>
        <email>...</email>
        <phone>...</phone>
    </xml>

## POST /user/

Registers a new user

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "email":"...","password":"...","name":"...", "phone":"...", "address":"..." https://www.caninecompany.com/api/v1/user

#### response
    <xml>
        <status>success</status>
        <user_id>...</user_id>
        <token>auth token</token>
    </xml>

# Dogs

## GET /dog
Gets the list of dogs for the user.

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" https://www.caninecompany.com/api/v1/dog

#### response
    <xml>
        <status>success</status>
        <dogs>
            <dog_id>...</dog_id>
            <dog_id>...</dog_id>
        </dogs>
    </xml>

## GET /dog/:id
Gets dog details for the user.

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" https://www.caninecompany.com/api/v1/dog/:id

#### response
    <xml>
        <status>success</status>
        <name>...</name>
        <breed>...</breed>
        <sex>...</sex>
        <age>...</age>
        <status>...</status>
    </xml>

## POST /dog

Creates a new Dog record for the user

#### Parameters

###### name
###### breed
###### sex
###### age
###### status ( dead/alive,qualified for service) 

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" -X POST -d ... https://www.caninecompany.com/api/v1/dog

#### response
    <xml>
        <status>success</status>
        <dog_id>...</dog_id>
    </xml>

## PUT /dog/:id

Updates existing Dog record for the user

#### Parameters

###### dog_id
###### name
###### breed
###### sex
###### age
###### status ( dead/alive,qualified for service) 

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" -X PUT -d ... https://www.caninecompany.com/api/v1/dog/:id

#### response
    <xml>
        <status>success</status>
    </xml>
        
# Battery Plans

## GET /battery_plans

Get details about battery plan subscriptions for the user.

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/battery_plans

#### response
    <xml>
        <status>success</status>
        <subscriptions>
            <subscription>
                <battery_type>...<battery_type>
                <status>...</status>
                <expiration_date>...</expiration_date>
                <ship_count>...</ship_count>
                <frequency>...</frequency>
                <last_shipment_date>...</last_shipment_date>
                <next_shipment_date>...</next_shipment_date>
                <auto_renewal_status>...</auto_renewal_status>
                ...
            </subscription>
            ...
        </subscriptions>
    </xml>

# Service Plan

## GET /service_plan

Get details about user service plan.

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/service_plan

#### response
    <xml>
        <status>success</status>
        <service_plan>
                <status>...</status>
                <expiration_date>...</expiration_date>
                <auto_renewal_status>...</auto_renewal_status>
                <num_pets>...</num_pets>
                ...
        </service_plan>
    </xml>

# Warranty

## GET /warranty

Get details about user warranties

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/warranty

#### response
    <xml>
        <status>success</status>
        <products>
            <product>
                <name>...</name>
                <serial_number>...</serial_number>
                <expiration_date>...</expiration_date>
                <auto_renewal_status>...</auto_renewal_status>
                <warranty_status>...</warranty_status>
                <purchase_date>...</purchase_date>
                ...
                </product>
                ...
        </products>
    </xml>

# History

## GET /history

Gets user history

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/history

#### response
    <xml>
        <status>success</status>
        <items>
            <item>
                <date>...</date>
                <type>...</type>
                <rep_name>...</rep_name>
                <notes>...</notes>
                <invoice_items>...</invoice_items>
                <time>...</time>
                <delivery_address>...</delivery_address>
                <shipment_tracking_info>...</shipment_tracking_info>
                ...
                </item>
                ...
        </items>
    </xml>

# ECommerce

## GET /ccdetails

Gets user credit card details

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/ccdetails

#### response
    <xml>
        <status>success</status>
        <cards>
        <card>
        ...
        </card>
        ...
        </cards>
    </xml>

## POST /ccdetails

Adds new credit card to user

#### Parameters

###### cardnumber
###### name
###### expirydate
###### CVC code
###### Billing address if different from user address

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "cardnumber":"...","name":"...","expirydate":"...","cvc":"...","address":"..."  https://www.caninecompany.com/api/v1/ccdetails


#### response
    <xml>
        <status>success</status>
    </xml>

# Booking/Purchase

## Invisible Fence Service

## GET /fence_service/available_dates

Gets the available date/time for fence service.

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" https://www.caninecompany.com/api/v1/fence_service/available_dates

#### response
    <xml>
        <status>success</status>
        <available_datetime>...</available_datetime>
        <cost>...</cost>
        ...
    </xml>

## POST /fence_service/lock_time

Service used to temporarily lock the appointment time while the user is entering other details.

#### Parameters

###### date
###### time

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "date":"...","time":"..." ... https://www.caninecompany.com/api/v1/fence_service/lock_time

#### response
    <xml>
        <status>success</status>
    </xml>

## POST /fence_service/unlock_time

Service used to unlock the appointment time if the user cancels the process.

#### Parameters

###### date
###### time

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "date":"...","time":"..." ... https://www.caninecompany.com/api/v1/fence_service/unlock_time

#### response
    <xml>
        <status>success</status>
    </xml>



## POST /fence_service/booking

Service used to create a new fence service appointment.

#### Parameters

###### date
###### time
###### reason ( Upgrade, change layout, repair, other)
###### address
###### cc info
###### more than 3 acres?
###### major changes to property?
###### dog crossed boundary?
###### additional info
###### notification preference ( email,phone,SMS)

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "date":"...","time":"..." ... https://www.caninecompany.com/api/v1/fence_service/booking

#### response
    <xml>
        <status>success</status>
        <confirmation_number>...</confirmation_number>
    </xml>

## Spa

## GET /spa_service/available_dates

#### Parameters

###### zipcode
###### dog_id - one or more

Gets the available date/time for Spa service.

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" https://www.caninecompany.com/api/v1/spa_service/available_dates?zipcode=...&dog_id=[...]

#### response
    <xml>
        <status>success</status>
        <available_datetime>...</available_datetime>
        <cost>...</cost>
        ...
    </xml>

## GET /spa_service/available_addons

#### Parameters

###### zipcode
###### dogid

Gets the available addon services.

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" https://www.caninecompany.com/api/v1/spa_service/available_addons?zipcode=...

#### response
    <xml>
        <status>success</status>
        <services>
        ...
        </services>
    </xml>

## POST /spa_service/lock_time

Service used to temporarily lock the appointment time while the user is entering other details.

#### Parameters

###### date
###### time

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "date":"...","time":"..." ... https://www.caninecompany.com/api/v1/spa_service/lock_time

#### response
    <xml>
        <status>success</status>
    </xml>

## POST /spa_service/unlock_time

Service used to unlock the appointment time if the user cancels the process.

#### Parameters

###### date
###### time

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "date":"...","time":"..." ... https://www.caninecompany.com/api/v1/spa_service/unlock_time

#### response
    <xml>
        <status>success</status>
    </xml>

## POST /spa_service/booking

Service used to create a new Spa appointment.

#### Parameters

###### date
###### time
###### pets
###### addon
###### additional info
###### notification preference ( email,phone,SMS)

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "date":"...","time":"..." ... https://www.caninecompany.com/api/v1/spa_service/booking

#### response
    <xml>
        <status>success</status>
        <confirmation_number>...</confirmation_number>
    </xml>

# Notifications

## GET /notifications

Gets notifications for the user. This will be called periodically from the app server. This will be used to retrieve Flash sales, promotional offers, Rep job completion status, battery, service plan renewal notifications, Rep arrival time and Seasonal alerts.

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/notifications

#### response
    <xml>
        <status>success</status>
        <notifications>
        <notification>
        <image>...</image>
        <message>...</message>
        <type>...</type>
        <link>...</link>
        ...
        </notification>
        ...
        </notifications>
    </xml>

# Tips & Tricks

## GET /tips

Retrieves Tips & Tricks 

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/tips

#### response
    <xml>
        <status>success</status>
        <tips>
        <tip>
        <image>...</image>
        <message>...</message>
        <type>...</type>
        <link>...</link>
        ...
        </tip>
        ...
        </tips>
    </xml>

# Seasonal Information

## GET /seasonalinfo

Retrieves Seasonal Info

#### example request

    $ curl -H "Authentication: hmac auth token digest" -H "Accept: application/xml" https://www.caninecompany.com/api/v1/seasonalinfo

#### response
    <xml>
        <status>success</status>
        <items>
        <item>
        <name>...</name>
        <image>...</image>
        <desc>...</desc>
        <type>...</type>
        <link>...</link>
        ...
        </item>
        ...
        </items>
    </xml>

# Photo Fun

## POST /photo

Uploads photo to CC for approval
#### Parameters

###### image file

#### example request

    $ curl -H "Accept: application/xml" -X POST -d "name":"...","desc":"..." --data-binary @"...image file path..." https://www.caninecompany.com/api/v1/photo


#### response
    <xml>
        <status>success</status>
    </xml>

# Pet friendly locations

## GET /petfriendlylocations

Retrieves Pet friendly locations

#### Parameters

###### latitude
###### longitude

#### example request

    $ curl -H "Authentication:..." -H "Accept: application/xml" https://www.caninecompany.com/api/v1/petfriendlylocations?latitude=...&longitude=...

#### response
    <xml>
        <status>success</status>
        <locations>
            <location>...</location>
        ...
        </locations>
    </xml>

## POST /petfriendlylocation
Uploads pet friendly location details

#### Parameters

######  name
######  type ( Restaurant, dog park, hotel, beaches, national park, other ...)
######  address

#### example request
    $ curl -H "Accept: application/xml" -X POST -d "name":"...","type":"..." ...  https://www.caninecompany.com/api/v1/petfriendlylocation

#### response
    <xml>
        <status>success</status>
    </xml>
