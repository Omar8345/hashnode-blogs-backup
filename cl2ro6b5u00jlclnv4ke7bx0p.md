## How is it easy to use an "API"?

Wondering all the time on how to use **APIs**? Do you find it challenging **all time**?

**Stay right there! We will be explaining:**

- **What is an API?**
- **API useful cases**

Ahem, without further ado, let's get into it!

-----------------------------------------------------------------

## What is an API?

API which stands for **Application Programming Interface**. An **API** allows *apps to connect with each other*. 

Ok, now we know what is **API** and what it actually does? I want to learn more, let's hand out an example!

Imagine you are in an online store, it's name is **Hashnode Swag Store**, I will be buying 2 T-Shirts and 3 pens, with the total price of **50$**. The store wants to uses a service to process **Credit/Debit card payments...** The store uses **[Stripe](https://www.stripe.com/)** to **process payments**, they prefer that the user **stays on there store website, and not to redirect to a different page.** Here is the work of **API**. The store will use **[Stripe's API](https://stripe.com/docs/api)** to handle the payment.

The payment flow as follows:

**`Payment info given to the store by the customer => The store sends a request to Stripe to process payment in addition to provides payment info => Stripe replies with a successful payment message => The store confirms the payment has been successful`**

All of this process, the store is using **Stripe API** to process payment, the user stays on the same page, and the processing happens using the **API at the backend.**

-----------------------------------------------------------

## API useful cases

We will be using **APIs** with 3 different cases:

- **Make a Zoom Meeting using Zoom API**
- **Get Real-time Crypto price using Binance API**
- **Get Weather using OpenWeathermap API**

## Make a Zoom Meeting using Zoom API

For **Zoom API Developer Docs, [click here](https://marketplace.zoom.us/docs/api-reference/zoom-api/)**.

Now, let's explain the case.

I need to make a Python simple script, when it is executed, it needs to use the **Zoom API** to generate a meeting link, we will be using the most user-friendly, easy-to-learn, and popular programming language **Python**. 

Steps:

- **[Sign up or Sign in to use the API](https://marketplace.zoom.us/)**

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651666968173/iwpCieIjD.png align="left")

- **Click on Develop, then click Build App**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651667122641/VLS2rdgpw.png align="left")

- **Agree to the "Zoom’s API License and Terms of Use"**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651667181114/t8T5qAd6A.png align="left")

- **Choose the the app type to be `JWT` - Why? `JWT` is easy-to-use (Click Create)**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651667284244/5_kTHDNZ1.png align="left")

- **Enter the name of your application - For example: Zoom Meeting Generator**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651667358092/nJSL7PSVm.png align="left")

- **Enter some mandatory details (Done individually)**

- **After filling the required info, go to App Credentials - Copy the API Key and the API Secret**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651667566675/bJxF2BzVI.png align="left")

We are done from the step to do on **Zoom website** till now. Now, we need to install 2 **Python** packages.

- **JWT - `pip install PyJWT`**
- **Requests - `python -m pip install requests`**

Done? Let's start coding!

First, let's make our code start:

```py
import jwt
import requests
import json
from time import time


# Enter your API key and your API secret
API_KEY = 'Your API key'
API_SEC = 'Your API secret'
```

Here, we imported all the libraries we need, and we made 2 variables, `API_KEY` and `API_SEC`, replace the `API_KEY` and `API_SEC` with your own keys.

```py
def generateToken():
	token = jwt.encode(

		# Create a payload of the token containing
		# API Key & expiration time
		{'iss': API_KEY, 'exp': time() + 5000},

		# Secret used to generate token signature
		API_SEC,

		# Specify the hashing alg
		algorithm='HS256'
	)
	return token
```

Here, we are generating the token.

```
# create json data for post requests
meetingdetails = {"topic": "The title of your zoom meeting",
				"type": 2,
				"start_time": "2019-06-14T10: 21: 57",
				"duration": "45",
				"timezone": "Europe/Madrid",
				"agenda": "test",

				"recurrence": {"type": 1,
								"repeat_interval": 1
								},
				"settings": {"host_video": "true",
							"participant_video": "true",
							"join_before_host": "False",
							"mute_upon_entry": "False",
							"watermark": "true",
							"audio": "voip",
							"auto_recording": "cloud"
							}
				}
```

Here, this is a sample data (**JSON**) for our **POST** request.

```py
def createMeeting():
	headers = {'authorization': 'Bearer ' + generateToken(),
			'content-type': 'application/json'}
	r = requests.post(
		f'https://api.zoom.us/v2/users/me/meetings',
		headers=headers, data=json.dumps(meetingdetails))

	print("\n creating zoom meeting ... \n")
	# print(r.text)
	# converting the output into json and extracting the details
	y = json.loads(r.text)
	join_URL = y["join_url"]
	meetingPassword = y["password"]

	print(
		f'\n here is your zoom meeting link {join_URL} and your \
		password: "{meetingPassword}"\n')


# run the create meeting function
createMeeting()
```

Here is our main function, creating the meeting and also, we won't forget to run the function `createMeeting` to create our fancy Zoom meeting. When the application is executed, meeting details are provided in the terminal in addition to the meeting is scheduled on your Zoom account you used at (marketplace.zoom.us).

Let's give it a test. Here is a quick video.

%[https://player.vimeo.com/video/706127303?h=1a8340f117&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479]

Here is a documentation on **Zoom Docs**: [**Create a meeting**](https://marketplace.zoom.us/docs/api-reference/zoom-api/methods/#operation/meetingCreate)

Full code:

```py
import jwt
import requests
import json
from time import time


# Enter your API key and your API secret
API_KEY = 'Your API key'
API_SEC = 'Your API secret'

# create a function to generate a token
# using the pyjwt library


def generateToken():
	token = jwt.encode(

		# Create a payload of the token containing
		# API Key & expiration time
		{'iss': API_KEY, 'exp': time() + 5000},

		# Secret used to generate token signature
		API_SEC,

		# Specify the hashing alg
		algorithm='HS256'
	)
	return token


# create json data for post requests
meetingdetails = {"topic": "The title of your zoom meeting",
				"type": 2,
				"start_time": "2019-06-14T10: 21: 57",
				"duration": "45",
				"timezone": "Europe/Madrid",
				"agenda": "test",

				"recurrence": {"type": 1,
								"repeat_interval": 1
								},
				"settings": {"host_video": "true",
							"participant_video": "true",
							"join_before_host": "False",
							"mute_upon_entry": "False",
							"watermark": "true",
							"audio": "voip",
							"auto_recording": "cloud"
							}
				}

# send a request with headers including
# a token and meeting details


def createMeeting():
	headers = {'authorization': 'Bearer ' + generateToken(),
			'content-type': 'application/json'}
	r = requests.post(
		f'https://api.zoom.us/v2/users/me/meetings',
		headers=headers, data=json.dumps(meetingdetails))

	print("\n creating zoom meeting ... \n")
	# print(r.text)
	# converting the output into json and extracting the details
	y = json.loads(r.text)
	join_URL = y["join_url"]
	meetingPassword = y["password"]

	print(
		f'\n here is your zoom meeting link {join_URL} and your \
		password: "{meetingPassword}"\n')


# run the create meeting function
createMeeting()
```

## Get Real-time Crypto price using Binance API

We will be getting the price of **BTC (Bitcoin)** in this case because it is so popular.

Before we start, be sure to install:

- **Requests - `python -m pip install requests`**

We will start with the basics.

```py
# Import libraries
import json
import requests
  
# defining key/request url
key = "https://api.binance.com/api/v3/ticker/price?symbol=BTCUSDT"
```

Here, we defined the request URL in addition to imported the nesseccary libraries.

```py
# requesting data from url
data = requests.get(key)  
data = data.json()
print(f"{data['symbol']} price is {data['price']}")
```

This is the final piece of code, here we requested **BTC (Bitcoin)** price (live price - current price) in **USD (United States Dollars)** from the request URL and printed them in an format which we could actually understand.

Let's try it, here is a quick test video!

%[https://vimeo.com/706137476]

You can notice I wait few seconds before running the script again, as you can see the price keeps changing which actually tells us it gets it every time, it should be updated and printed afterwards. Also, we used `{data['symbol']}` so that if someone changes the currency, it will update the currency also when it is printing the output.

Full code:

```py
# Import libraries
import json
import requests
  
# defining key/request url
key = "https://api.binance.com/api/v3/ticker/price?symbol=BTCUSDT"

# requesting data from url
data = requests.get(key)  
data = data.json()
print(f"{data['symbol']} price is {data['price']}")
```

## Get Weather using OpenWeathermap API

Before we start, get your own **API** key from [here](https://openweathermap.org/api).

Done? Now we need to install a module:

- **Requests - `python -m pip install requests`**

Let's start:

```py
# Python program to find current
# weather details of any city
# using openweathermap api
 
# import required modules
import requests, json
 
# Enter your API key here
api_key = "Your_API_Key"
 
# base_url variable to store url
base_url = "http://api.openweathermap.org/data/2.5/weather?"
```

Here, we imported modules, set our **API key**, and **REQUEST URL**.

```
# Give city name
city_name = input("Enter city name : ")
 
# complete_url variable to store
# complete url address
complete_url = base_url + "appid=" + api_key + "&q=" + city_name
 
# get method of requests module
# return response object
response = requests.get(complete_url)
 
# json method of response object
# convert json format data into
# python format data
x = response.json()
 
# Now x contains list of nested dictionaries
# Check the value of "cod" key is equal to
# "404", means city is found otherwise,
# city is not found
if x["cod"] != "404":
 
    # store the value of "main"
    # key in variable y
    y = x["main"]
 
    # store the value corresponding
    # to the "temp" key of y
    current_temperature = y["temp"]
 
    # store the value corresponding
    # to the "pressure" key of y
    current_pressure = y["pressure"]
 
    # store the value corresponding
    # to the "humidity" key of y
    current_humidity = y["humidity"]
 
    # store the value of "weather"
    # key in variable z
    z = x["weather"]
 
    # store the value corresponding
    # to the "description" key at
    # the 0th index of z
    weather_description = z[0]["description"]
 
    # print following values
    print(" Temperature (in kelvin unit) = " +
                    str(current_temperature) +
          "\n atmospheric pressure (in hPa unit) = " +
                    str(current_pressure) +
          "\n humidity (in percentage) = " +
                    str(current_humidity) +
          "\n description = " +
                    str(weather_description))
 
else:
    print(" City Not Found ")
```

Here, we completed the rest of the code, this piece of code asks for the city name, completes the **REQUEST URL** with the needed value to get back the expected response, convert response from **JSON** to **Python** format, if city not found, we get 404, but we return in the console city not found, and if it was found, it stores weather details and return them.

Here is a quick testing video.

%[https://player.vimeo.com/video/706146344?h=d492ae72db&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479]

Full code:

```py
# Python program to find current
# weather details of any city
# using openweathermap api
 
# import required modules
import requests, json
 
# Enter your API key here
api_key = "Your API key"
 
# base_url variable to store url
base_url = "http://api.openweathermap.org/data/2.5/weather?"

# Give city name
city_name = input("Enter city name : ")
 
# complete_url variable to store
# complete url address
complete_url = base_url + "appid=" + api_key + "&q=" + city_name
 
# get method of requests module
# return response object
response = requests.get(complete_url)
 
# json method of response object
# convert json format data into
# python format data
x = response.json()
 
# Now x contains list of nested dictionaries
# Check the value of "cod" key is equal to
# "404", means city is found otherwise,
# city is not found
if x["cod"] != "404":
 
    # store the value of "main"
    # key in variable y
    y = x["main"]
 
    # store the value corresponding
    # to the "temp" key of y
    current_temperature = y["temp"]
 
    # store the value corresponding
    # to the "pressure" key of y
    current_pressure = y["pressure"]
 
    # store the value corresponding
    # to the "humidity" key of y
    current_humidity = y["humidity"]
 
    # store the value of "weather"
    # key in variable z
    z = x["weather"]
 
    # store the value corresponding
    # to the "description" key at
    # the 0th index of z
    weather_description = z[0]["description"]
 
    # print following values
    print(" Temperature (in kelvin unit) = " +
                    str(current_temperature) +
          "\n atmospheric pressure (in hPa unit) = " +
                    str(current_pressure) +
          "\n humidity (in percentage) = " +
                    str(current_humidity) +
          "\n description = " +
                    str(weather_description))
 
else:
    print(" City Not Found ")
```

## The End! 🚀🎉

Thanks for reading my article! I hope you like it!

Do you have any errors when using our test cases code? Comment them down below or create an issue on the GitHub Repo.

[**Code GitHub Repo**](https://github.com/OmarDev100/how-to-use-api)