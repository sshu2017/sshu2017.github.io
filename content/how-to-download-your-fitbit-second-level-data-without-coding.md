Title: How to Download Your Fitbit Second-Level Data Without Coding
Date: 2016-06-16 21:45
Author: shushi2000
Category: General, Python
Slug: how-to-download-your-fitbit-second-level-data-without-coding
Status: published

If you are a Fitbit user who wants to save a copy of Fitbit data on your computer but doesn't have advanced programming skills , this tutorial is right for you! You don't need to do any coding at all to save your second-level data. I have been struggling with getting all the so-called 'intraday data' for quite a while. I have found many useful resources online, for example, [Paul's tutorial](http://pdwhomeautomation.blogspot.com/2015/03/sleep-infographic-using-raspberry-pi.html),  [Collin Chaffin's Powershell module](https://github.com/CollinChaffin/psFitb1t), and the [Fitbit-Python API](https://github.com/orcasgit/python-fitbit), but they are somehow complicated and I just could not make any of these working for me smoothly.  Recently I finally figured out a way to download these Fitbit data without any coding. Are you ready?

**Step 1: Register an app on <http://dev.fitbit.com>**

First you need to register an account on [dev.fitbit.com](http://dev.fitbit.com), and then click 'MANAGE YOUR APPS' on the top right area. Next you need to click 'Register a new app' button at the top right area to start with. Well, this step is simple, just make sure the OAuth 2.0  Application Type is set to 'Personal', and the Callback URL is complete - including the 'http://' part and also a '/' at the end. Here I used 'http://google.com/' as an example. I have used this blog's URL 'http://shishu.info/' which worked just fine too.

[![app2](http://shishu.info/wp-content/uploads/2016/06/app2.jpg){.aligncenter .size-full .wp-image-195 width="749" height="937"}](http://shishu.info/wp-content/uploads/2016/06/app2.jpg)

After you click the red 'Register' button, you will be able to see the credentials for the app you just registered. The 'OAuth 2.0 Client ID' and 'Client Secret' will be used in the next step.

[![credentials2](http://shishu.info/wp-content/uploads/2016/06/credentials2.jpg){.aligncenter .size-full .wp-image-196 width="748" height="628"}](http://shishu.info/wp-content/uploads/2016/06/credentials2.jpg)

 

**Step 2: Use the OAuth 2.0 tutorial page**

Next you need to right click the 'OAuth 2.0 tutorial page' link and open it in a new tab, so that you can look back at your app's credentials easily. Make sure the 'Implicit Grant Flow' is chosen instead of 'Authorization Code Flow' - this will make things much easier! After you copy/paste the 'Client ID' and 'Client Secret' into the blanks and put in the Redirect URI, click the auto-generated link.

[![tutorial1](http://shishu.info/wp-content/uploads/2016/06/tutorial1.jpg){.aligncenter .size-full .wp-image-198 width="757" height="803"}](http://shishu.info/wp-content/uploads/2016/06/tutorial1.jpg)

Then you will see the confirmation page. Just click 'Allow'.

[![confirmation](http://shishu.info/wp-content/uploads/2016/06/confirmation.jpg){.aligncenter .size-full .wp-image-199 width="495" height="579"}](http://shishu.info/wp-content/uploads/2016/06/confirmation.jpg)

And you will be led to the 'Redirect URI', which is 'http://google.com/' in this case.  But the address bar now shows a very long string which is the token for your app.

[![token](http://shishu.info/wp-content/uploads/2016/06/token.jpg){.aligncenter .size-full .wp-image-200 width="1802" height="520"}](http://shishu.info/wp-content/uploads/2016/06/token.jpg)

Next you need to copy and paste everything in the address bar but without the starting part ( https://www.google.com/ ) to the 'Parse response' section, and hit enter key once. This way you can clearly see what the token is, what the scope is, and how long the token is valid. In this case, the token is valid for 1 week, which equals to 604800 seconds. Pretty good, right?

[![token2](http://shishu.info/wp-content/uploads/2016/06/token2.jpg){.aligncenter .size-full .wp-image-201 width="742" height="443"}](http://shishu.info/wp-content/uploads/2016/06/token2.jpg)

 

**Step 3: Make request and get the data!**

After you are done with the 'Parse response', the next step is ready for you automatically.

[![curl](http://shishu.info/wp-content/uploads/2016/06/curl.jpg){.aligncenter .size-full .wp-image-202 width="739" height="343"}](http://shishu.info/wp-content/uploads/2016/06/curl.jpg)

Justclick the 'Send to Hurl.it' link and 'Launch Request' in the new page. Make sure to tell the web that you are not a robot too.

[![Hurl\_it](http://shishu.info/wp-content/uploads/2016/06/Hurl_it.jpg){.aligncenter .size-full .wp-image-203 width="1827" height="792"}](http://shishu.info/wp-content/uploads/2016/06/Hurl_it.jpg)

After that, if you see the '200 OK' status - meaning everything works fine. And you can find the data you want in the lower half of the page. Like this:

[![body](http://shishu.info/wp-content/uploads/2016/06/body.jpg){.aligncenter .size-full .wp-image-204 width="1617" height="829"}](http://shishu.info/wp-content/uploads/2016/06/body.jpg)

If you click 'view raw' at the right side, you will see the 'BODY' will be changed to raw text file and you can simply copy / paste them to a text editor. And that's all you do to download your Fitbit second-level data! As I promised, you don't need to know any programming skills to accomplish this, isn't that cool?

**Additional tips:**

tip 1: other data types

If you want some other data rather than the 'user profile', you can simply change the 'API endpoint URL' in the 'Make Request' step. According the the [Fitbit API documentation](https://dev.fitbit.com/docs/), you can get the heart rate data by using this URL:

`https://api.fitbit.com/1/user/-/activities/heart/date/today/1d.json`

Or the sleep data by using:

`https://api.fitbit.com/1/user/28H22H/sleep/date/2014-09-01.json`

tip 2: save json file in an easier way

If you think the 'Send to Hurl.it' method is not fast enough, you can copy the 'curl' command auto-generated in the 'Make Request' step and run it in terminal (for Windows, that is the 'cmd' window). Add the following part to the end of the copied 'curl' command so that the data will be saved to your disk:

` >> data_file.json `

tip 3: save multiple days' data automatically

I think Fitbit provides the functionality to let uers download multiple days' data with one command, by specifying the date rage in the curl request. However I could not make it work for me for some unknown reason. Therefore I used a piece of Python code to download multiple days' data for me. Here's the code, which I think is pretty self-explanatory.

``` {lang="Python" line="0"}
import requests
import json
import pandas as pd
from time import sleep

# put the token for your app in between the single quotes
token = ''

# make a list of dates 
# ref: http://stackoverflow.com/questions/993358/creating-a-range-of-dates-in-python
# You can change the start and end date as you want
# Just make sure to use the yyyy-mm-dd format
start_date = '2015-12-28'
end_date = '2016-06-14'
datelist = pd.date_range(start = pd.to_datetime(start_date),
                         end = pd.to_datetime(end_date)).tolist()

'''
The codes below use a for loop to generate one URL for each day in the datelist,
and then request each day's data and save the data into individual json files.
Because Fitbit limit 150 request per hour, I let the code sleep for 30 seconds 
between each request, to meet this limitation.
'''
for ts in datelist:
    date = ts.strftime('%Y-%m-%d')
    url = 'https://api.fitbit.com/1/user/-/activities/heart/date/' + date + '/1d/1sec/time/00:00/23:59.json'
    filename = 'HR'+ date +'.json'
    response = requests.get(url=url, headers={'Authorization':'Bearer ' + token})
    
    if response.ok:
        with open(filename, 'w') as f:
            json.dump(response.content, f)
        print (date + ' is saved!')
        sleep(30)
    else:
        print ('The file of %s is not saved due to error!' % date)
        sleep(30)
```

Happy hacking!
