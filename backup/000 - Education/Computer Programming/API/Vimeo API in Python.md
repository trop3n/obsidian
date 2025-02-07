---
up: "[[API]]"
tags:
  - "#education/computerprogramming/API/vimeoAPIpython"
---


# Introduction to the Course

In November 2004, [Vimeo](https://vimeo.com/) started as a side project by two web developers to tag and share short videos. The name Vimeo originated from one of the founders when he combined words ‘video’ and ‘me’. Its business model is based on SaaS (Software as a Service). Vimeo provides tools to host, share, and create videos with a focus on delivering high-definition content to a range of devices. It also offers tools that let us create content, edit videos, broadcast, and more.

## Vimeo vs. YouTube

Let's see a brief comparison between Vimeo and YouTube in the table below:

| **Vimeo**                                                                               | **YouTube**                                                                                             |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Vimeo has a community of mature individuals who provide productive and useful feedback. | YouTube has a large community of mixed users compared to Vimeo, and their feedback isn’t always useful. |
| Vimeo offers free and paid tiers.                                                       | YouTube offers a free version with ads and an ad-free paid version.                                     |
| Vimeo offers to protect your video via a password.                                      |                                                                                                         |
## Prerequisites

In this course, we'll explore different endpoints of the Vimeo API. We'll make calls to the endpoints using HTTP requests in the Python programming language. Therefore, below are the requirements to take this course:

    A basic understanding of APIs
    A basic understanding of HTTP requests
    Fundamentals of Python programming language

## Intended Audience

This API course could be for the following people:

- A student with a basic knowledge of HTTP requests who wants to learn about APIs.
- Developers who want to explore and integrate the Vimeo API.
- A professional who has ample experience working with other APIs and wants to explore the Vimeo API.

# Get Started with the Vimeo API

Learn how to sign-up for Vimeo and get authenticated for Vimeo services.

In this lesson, we'll see the sign-up process of Vimeo and how to get authenticated to use Vimeo API services.
## Sign Up and Create an Application

You can sign up on the [Vimeo](https://vimeo.com/join) platform with the following steps:

- Provide a name, email ID, and password.
- After you have entered your information, a survey form is shown. You can either fill the form and continue or skip the form.
- The next screen will show Vimeo’s pricing plan, you don’t need to worry about that for this course.

A verification email is then sent to the registered email ID; click the link to verify the account. Once verified, you'll be redirected to Vimeo's homepage.

Next let’s create an application and generate an access token. To create an application, visit the [Vimeo developer](https://developer.vimeo.com/apps) page and follow the steps below:

1. Click "Create an app."
2. In the required "App name" field, name your application.
3. Briefly explain your application in the next required field, “App description.” The users see this description when your application asks permission to access their account.
4. Next, decide about the access permissions for your application. Select the "No" option, check the agreement statement, and click the "Create App" button.

Congratulations! Your application has been created.

## Generate an Access Token

Next, we’ll generate an access token for the application. Follow the steps below to generate a token:

1. Click your application to view the details.
2. On the setting page of your application, navigate to the "Generate Access Token" section.
3. Here you see two options, "Authenticated (you)" and "Unauthenticated." The “Authenticated: option will allow access to your private data—for this course, you’ll need to select this option.
4. This will expand the "Scopes" section—check the "Private" scope in addition to the "Public".
5. Once you have checked "Private," more scopes will appear check all of them and click on the "Generate" button.
6. This generates a token that is visible for the first time only. It is recommended to save this token somewhere safe.

## Test our Configuration and Get USER_ID

To use Vimeo APIs, we need to send a request to the `base_url` shown in the cod block below.

```python
base_url = https://api.vimeo.com/
```

Click the edit button in the widget below and save the copied token as `AUTH_CODE` to use it throughout the course. Next, let's test our authentication code by executing the code widget below, which automatically extracts the user ID and assigns it to `USER_ID`. Click the "Save" button so we have the user ID available throughout the course.

There is a brief description of categories, channels, videos and groups in the table below:

| **Vimeo's resource** | **Description**                                                                                                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Categories           | A category defines a set of videos that belong to a specific genre.                                                                 |
| Channels             | This resource arranges videos based on their theme or some other criteria and groups them in Channels.                              |
| Videos               | Videos are the main content on Vimeo.                                                                                               |
| Groups               | Groups are the places like communities where the members can share, discuss, and collaborate on videos according to their likeness. |
# Vimeo Categories

## List Categories and Get Category Details

Learn how to list categories and extract details of those categories using the Vimeo API.
### Overview

This lesson will provide a brief overview of important endpoints from the categories section of the Vimeo API. A category defines a set of videos that belong to a specific genre. When videos are categorized, it's easier to find the information according to our interests. 

In this less, we'll use the following two endpoints:

- We'll use the `{base_url}/categories` endpoint to get all categories.
- We'll use the `{base_url]/categoires/{category name}` endpoint to get to a specific category.
### Get All Categories

First, we'll extract all the categories available on Vimeo. To do this we use the `{base_url}/categories` endpoint, which utilizes the HTTP `GET` request method.
#### Request Parameters

Since it's a `GET` request, the endpoint doesn't take any parameter in the body of the request. However, some filters are available that we can apply as query parameters. Some of these parameters are listed in the table below:

| Parameter Name | Type     | Category | Description                                                                                                           |
| -------------- | -------- | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `direction`    | String   | Optional | This parameter defines the order in which we want the response. The possible values are `asc` and `desc`.             |
| `page`         | Integer  | Optional | This defines the page number we want to display in the response.                                                      |
| `per_page`     | Integeer | Optional | This parameter defines how many records we want to show on one page. A maximum of 100 records can be shown on a page. |
Let's see how the category endpoint works in the code widget below:

```python
import requests
import json

url = "https://api.vimeo.com/categories"
# url = "https://api.vimeo.com/categories?direction=asc&page=2&per_page=5"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
```

Let's have a look at the highlighted lines in the code widget shown above:

1. **Lines 1-2**: We import the libraries required to make this call. These will be a part of every call, so we'll hide them in the next code widgets. 
2. **Lines 4-5**: We define the endpoint for this call. First we make a call with no filters, but in **line 5** we use the query parameters explained in the above table. We make the call on **line 4** by default, but to check **line 5**'s functionality feel free to uncomment it and comment **line 4** instead.
3. **Lines 7-10**: We define the `headers` object of the request that contains `Content-Type` in **line 8**, and then define `Authorization` in **Line 9**. 
4. **Line 12**: We make a `GET` request to the defined `url`.
5. **Lines 13-14**: We check the `status_code` of response in the `if` structure and print the statement accordingly.
6. **Line 16**: We print the data returned by this call.
### Response Fields

The successful execution of the above code will return metadata of the categories. Let's see some of the important fields from the response in the table below:

| Response Field             | Description                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `total`                    | The total number of items/categories. Its value is `10` because Vimeo has total of 10 categories.               |
| `page`                     | This shows the number of pages we get in the response.                                                          |
| `per_page`                 | This field shows the number of records/categories.                                                              |
| `data`                     | An array that contains all the fields related to categories.                                                    |
| `uri`                      | A unique identifier that can be used to access the category. The base URL isn't a part of the `uri`.            |
| `name`                     | This field states the name of the category.                                                                     |
| `link`                     | A complete URL of the category. We can copy and paste it into the browser's address bar to access the category. |
| `last_video_featured_time` | This field shows the ISO 8601 format of the time when the video was recently featured.                          |
| `metadata`                 | An object that contains the metadata related to a category.                                                     |
| `subcategories`            | An array that lists all the available subcategories within a main category.                                     |
### Get a Specific Category

Now that we have a list of all the categories, let's pick one category and get all the details related to that category. We'll use the `{base_url}/categories/{category_name}` endpoint. 
#### Request Parameters

Since this is an HTTPS `GET` request, it doesn't take a parameter in the request's body. However the name of the category is passed as a path parameter. In code below, we'll use the `adsandcommericals` category.

```python
url = "https://api.vimeo.com/categories/adsandcommercials"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")
    
print(json.dumps(response.json(), indent=4))
```

In the above code, we hide the import library to keep the code clean and concise. The highlighted lines of the code are explained below:

- **Line 1**: We define the `url` for this call, and append a specific category, `adsandcommericals`, in the URL as a path parameter.
- **Line 8**: We make a `GET` request to the `url` defined in **line 1**, and pass the authorization details through `headers`.
- **Line 12**: We print the response.
#### Response Fields

The response fields produced by this endpoint are almost he same as the "get all categories" endpoint, but some fields of the `metadata` object are listed in the table below:

| Field Name                                | Description                                                                                                                                                                                                                                                   |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `metadata.connections`                    | This object contains information associated with this category.                                                                                                                                                                                               |
| `metadata.connections.channels`           | This object gives information related to the channels in this category. It includes `uri` = a URL to get the channels in this category, `options` = an array of `HTTP` methods that can be performed on this URL, and `total` = the total number of channels. |
| `metadata.connections.groups`             | This object contains information related to the groups of the category. It also contains `url`, `options` and `total` fields.                                                                                                                                 |
| `metadata.connections.users`              | This object contains the information related to the users of this category.                                                                                                                                                                                   |
| `metadata.connections.videos`             | This object defines the uri, permitted methods, and the total number of videos related to this category.                                                                                                                                                      |
| `metadata.interactions`                   | This object shows the allocated actions related to the category.                                                                                                                                                                                              |
| `metadata.interactions.follow`            | This object shows the information whether the authenticated user follows this category or not.                                                                                                                                                                |
| `metadata.interactions.follow.added`      | This boolean field shows if the user has followed the category. If followed, its value will be `true` and `false` otherwise.                                                                                                                                  |
| `metadata.interactions.follow.added_time` | A string field specifying a time in ISO 8601 format when the authenticated user has performed the follow operation on this category.                                                                                                                          |
| `metadata.interactions.follow.uri`        | A link to the category if a user wants to follow or unfollow a category. The user can make a `PUT` request to this `uri` to follow and a `DELETE` request to unfollow this category.                                                                          |
## Get All Channels and Groups in a Category

Learn how to get all the channels and groups in a category using Vimeo API.

### Overview

In this lesson, well use two endpoints of categories.

- We’ll use the `{base_url}/categories/{category_name}/channels` endpoint to get all channels in a category.
- We’ll use the `{base_url}/categories/{category_name}/groups` endpoint to get all groups in a category.
### Get all Channels in a Category

We'll use the `categories/{category_name}/channels` endpoint to get all the channels available in category defined by the path parameter `{category_name}`.
### Request Parameters

This endpoint also utilizes an HTTP `GET` request, so the request's body is empty. However, this endpoint does take one required path parameter, `{category_name}`, and supports query parameters. Some of these query parameters are in the table below: 

| Parameter Name | Type    | Category | Description                                                                                                           |
| -------------- | ------- | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `direction`    | String  | Optional | This parameter defines the sorting direction of the results. It can have either of these two values: `asc` or `desc`. |
| `page`         | Integer | Optional | This integer value tells the request to show only the specified page.                                                 |
| `per_page`     | Integer | Optional | This value tells how many records we want on a single page.                                                           |
| `query`        | String  | Optional | This search query is used to filter the results.                                                                      |
Let's see the code below to get all the channels in a category.

```python
url = "https://api.vimeo.com/categories/adsandcommercials/channels"
# url = "https://api.vimeo.com/categories/adsandcommercials/channels?direction=asc&page=3"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: We define a URL that does not contain any request parameter. 
- **Line 2**: We define a URL with two query parameters, the first is `direction` and the other is `page`. We have commented this line out. To execute it, feel free to uncomment it and comment out line 1.
- **Line 9 and 13**: We create a `GET` request and print the response, respectively. 
### Response Fields

The successful execution of the above code returns all the channels in the `data` array. Let's see some important fields related to a channel from the `data` array in the table below:

| Response Field  | Description                                                                               |
| --------------- | ----------------------------------------------------------------------------------------- |
| `uri`           | A unique identifier, without a base URL, to access the channel resources.                 |
| `name`          | This field displays the name of the channel.                                              |
| `description`   | This field briefly describes the channel.                                                 |
| `link`          | A complete Vimeo link to the channel.                                                     |
| `created_time`  | A string of time in ISO 8601 format that shows the channel's creation timestamp.          |
| `modified_time` | A string of time in ISO 8601 format that tells about the last modified timestamp.         |
| `user`          | An object comprises information related to an authenticated user.                         |
| `websites`      | An array of all the websites that an authenticated user has added to their Vimeo profile. |
| `metadata`      | An object consists of all the information related to an authorized user.                  |
### Get All Groups in a Category

We use the `/categories/{category_name}/groups` endpoint to retrieve all the groups available in a category. The call returns the metadata and other information related to the groups, so a user can find and join a group of interest using its link.
#### Request Parameters

This endpoint also utilizes the HTTP `GET` request. Therefore, it doesn't take body parameters, but we'll pass one required parameter, `{category_name}`, as a path parameter. We can also use the same query parameters from the previous section.

Let's execute the code below and see it's functionality.

```python
url = "https://api.vimeo.com/categories/adsandcommercials/groups"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")
    
print(json.dumps(response.json(), indent=4))
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: This shows the `url` that we'll make a call to in order to get all the groups.
- **Lines 8 and 12**: These are the `GET` requests and the print statement for the response respectively. 
#### Response Fields

The successful execution of the above code returns all the groups from the given category. Let's see some new important response fields from the `data` array in the table below.

| **Response field** | **Description**                                                                                                                                                                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `privacy`          | An object that contains the privacy settings of a group.                                                                                                                                                                                         |
| `privacy.view`     | This field specifies the access permission for a group. Its value can be `anybody` or `members`. If the value is "anybody", it means that this group is accessible to everyone. If the value is "members" then only group members can access it. |
| `privacy.join`     | This field tells who can join this group; if the value is `anybody`, then anyone can join the group, and if the value is `members` then only group members can join this group.                                                                  |
| `privacy.invite`   | This field shows who can invite new members to the group. If its value is `all` then anyone can invite new members and if its value is `members` then only group members can invite new members.                                                 |
| `metadata`         | An object that contains metadata of the group like `users`, `videos`, and `interactions`.                                                                                                                                                        |
| `user`             | An object that comprises of information related to the group owner.                                                                                                                                                                              |
## User Operations on the Category

Learn how to perform some important operations on categories using the Vimeo API.
### Overview

In this lesson, we'll learn about a few-user related operations on a category:

- Check if a user follows a specific category
- Allow a user to follow a specific category
- Allow a user to unfollow a specific category
- Get all the categories that a user follows

We'll use the following endpoints to perform these operations:

- We'll use the `{base_url}/users{USER_ID}/categories/{category_name}` endpoint to check, follow and unfollow a category.
- We'll use the `{base_url}/users/{USER_ID}/categories` endpoint to get all categories followed by a user.
### Check, Follow and Unfollow a Category

In this section, we'll go over operations that we perform with the `users/{USER_ID}/categories/{category_name}` endpoint. This endpoint supports three functionalities which are specified by the type of HTTP method. Here `USER_ID` is the unique identifier of the authenticated ser, which is your ID.
#### Make a `GET` Request

When we an HTTPS `GET` request to this endpoint, it checks if the user associated with `USER_ID` has followed the category defined by `category_name`. It doesn't take body or query parameters, but `USER_ID` and `category_name` are required path parameters.

Let's see the functionality of the `GET` request in the code widget below.

```
USER_ID = 222656854
```

```python
url = "https://api.vimeo.com/users/{{USER_ID}}/categories/adsandcommercials"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 204:
    print("Following response is produced")
    print(json.dumps(response.json()['developer_message'], indent=4), "Response code: ", response)
else:
    print("Response code: ", response)
```


- **Line 1**: We define the `url`
- **Line 8**: We use the `url` to make a `GET` request
- **Line 13**: We print the response.
#### Response

The execution of the above code gives the HTTP code `404`. This means that the user isn't following this category. Now, let's make the user follow this category using a `PUT` request.
### Make a `PUT` Request

In this subsection, we'll use the same endpoint as before, but this time the request type is `PUT`. Now that we've verified that you don't follow the `adsandcommericals` category, let's follow this category.

```python
url = "https://api.vimeo.com/users/222656854/categories/adsandcommercials"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("PUT", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced")
    print(json.dumps(response.json(), indent=4))
else:
    print("Response code: ", response)
```
#### Response

The execution of the above code gives the HTTP code `204`. This means that the user (you) is now following this category. Let's go back to the previous subsection and execute the `GET` request again to see if the user has followed the `adsandcommericals` category, and this time the response will be an HTTP code `204`. This response shows that you're now following the category.
### Make a `DELETE` Request

Executing the above code with `DELETE` request results in unfollowing the category. After following a category, replace `PUT` with `DELETE` in **line 8** and press "Run". The response is again an HTTP code `204`. This means that the user has unfollowed the specified category.
### Get All the Categories Followed by a User

In this section we'll get all the categories you've followed by using `{base_url}/users/{USER_UD}/categories` endpoint. Here, the USER_ID is the required path parameter. With the help of this endpoint, we'll get all the categories that you follow. This endpoint can also take the same query parameters from earlier in this lesson.

Let's see the working code below:

```python
url = "https://api.vimeo.com/users/222656854/categories"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")

print(json.dumps(response.json(), indent=4))
```

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** Shows the `url` that is used to get all the categories that fall under your "following" list.
- **Lines 8 and 12**: We define the `GET` request and print the response, respectively.
### Response fields

Let's see the response of the above code in the table below:

| **Response field** | **Description**                                                                                                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `total`            | This field shows the total number of records returned by this call.                                                                                                                            |
| `data`             | An array of fields that includes `uri`, `name`, `link`, `top_level`, `metadata`, and more fields of each followed category. We have already seen most of these fields in the previous lessons. |
## Operations on Videos for a Category

Learn how to perform different operations on videos available in a category using the Vimeo API.
### Overview

In this lesson, we'll see some of the very important video operations on the categories of Vimeo. We'll cover the below endpoints in this lesson:

- We use the `{base_url}/categories/{category_name}/videos` endpoint to get all videos in a category.
- We use the `{base_url}/categories/{category_name}/videos/{VIDEO_ID}` endpoint to get details of a single video in a category.
- We use the `{base_url}/videos/{VIDEO_URL}/categories` endpoint to get all categories of a video.
### Get All Videos in a Category

With the `categories/{category_names}/videos` endpoint, we'll get all the videos from the `adsandcommericals` category.
#### Request Parameters

This endpoint takes one required path parameter and a bunch of query parameters. Let's see some of them in the table below:

| Parameter Name      | Type    | Category | Description                                                                                                                                                                                                             |
| ------------------- | ------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `category_name`     | String  | Required | This should be passed as a path parameter specifying the Vimeo category.                                                                                                                                                |
| `filter`            | String  | Optional | This is a query parameter that filters the results based on two attributes. THe `conditional_featured` filter values returns featured videos, and the `embeddable` value returns embeddable videos.                     |
| `filter_embeddable` | Boolean | Optional | This is an optional parameter, but if the filter value is `embeddable` then it is required to specify its value. If its value is `true` then the results are filtered by embeddable videos and otherwise if it `false`. |

> [!NOTE]
> **Note**: Other query parameters like `direction`, `page`, `per_page`, `query` and `sort` have already been discussed earlier.

Now, let's see the functionality in the code below. The execution of the code below automatically extracts the ID of the first video in a widget after the response. Click the "Save" button to use this ID in the next section(s).

```python
url = "https://api.vimeo.com/categories/adsandcommercials/videos/"
# url = "https://api.vimeo.com/categories/adsandcommercials/videos/?filter=embeddable&filter_embeddable=true"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")
    print(json.dumps(response.json()['developer_message'], indent=4))
else:
    print(json.dumps(response.json(), indent=4))
```

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** We define a `url` without any query parameter. It’s a simple call to the endpoint with only the required parameter.
- **Line 2:** We define a `url` with query parameters as mentioned in the table above. This line is commented out, but you can uncomment it to check the functionality. To do this, you must comment **line 1** to avoid `url` conflict.
- **Lines 9 and 14:** We’ll use the `GET` method and print the response, respectively.
#### Response Fields

We've already gone over the important fields returned by this endpoint.
### Get Details of a Single Video

In this section, we'll get all the details of the video whose ID was extracted earlier. The endpoint `{base_url}/categories/{category_name/videos/{VIDEO_ID}` doesn't take the body and query parameters, but does take two required path parameters -- `category_name` and `VIDEO_ID`.

Let's see the code below.

```python
url = "https://api.vimeo.com/categories/adsandcommercials/videos/{{VIDEO_ID}}"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")

print(json.dumps(response.json(), indent=4))
```

The above code is easy to understand and requires no explanation. Let's talk about the response fields briefly. 
#### Response Fields

The successful execution of the code widget shown above returns a number of fields. Let's see some important fields in the table below:

| Response Field     | Description                                                                                                                                                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`             | A string-type field that tells the type of the video. Its value can be: `live` -- if this video belongs to a live event. `stock` -- if this video is a Vimeo Stock video. `video` -- if it is a standard Vimeo video. |
| `player_embed_url` | A string field that gives an embed link to the Vimeo player.                                                                                                                                                          |
| `duration`         | An integer field that specifies the video's duration in seconds.                                                                                                                                                      |
| `width`            | An integer field tells how many pixels are there in a video's width.                                                                                                                                                  |
| `language`         | A string-type field that defines the primary language of the video.                                                                                                                                                   |
| `height`           | An integer field that specifies the video's height in pixels.                                                                                                                                                         |
| `embed`            | This field gives an `iframe` to embed this video.                                                                                                                                                                     |
| `content_rating`   | An array of rating classes that are assigned to a video specifying what type of content this video has. Seven tags are available for this field; some are "advertisement", "drugs", "language", and "safe"            |
| `stats`            | An object that shows the analytics associated with the video. It tells the total number of times this video is played.                                                                                                |
| `user`             | An object field that gives the information related to the owner of the video.                                                                                                                                         |
### Get all Categories to Which a Video Belongs

In this section, we'll use the `videos/{VIDEO_ID}/categories` endpoint to retrieve all the categories of a video specified by `VIDEO_ID`. This endpoint utilizes the HTTP `GET` request, and doesn’t take body and query parameters. It only takes one required parameter, which is `VIDEO_ID`.

```python
url = "https://api.vimeo.com/videos/{{VIDEO_ID}}/categories"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")

print(json.dumps(response.json(), indent=4))
```

> The successful execution of the above code returns the total number of categories and a `data` array. The fields in the `data` array are very descriptive, and most of them have already been discussed.

# Vimeo Channels

## Create and Edit a Channel

Learn how to create a new channel and make edits to it using the Vimeo API.
### Overview

In this chapter, we’ll focus on some of the important operations for Vimeo channels. Channels are used to arrange videos by grouping them based on a theme or some other criteria. We can add personal and publicly available videos to our channel. Since we are using Vimeo’s basic plan for this course, we can create only one channel.

Let’s look at how to create a new Vimeo channel and how to make edits to it. We’ll use the following endpoints to perform these tasks.

- We’ll use the `{base_url}/channels` endpoint to create a new channel.
- We’ll use the `{base_url}/channels/{NEW_CHANNEL_ID}` endpoint to edit a channel.
### Create a New Channel

In this section, we'll use `{base_url}/channels` endpoint to create a new channel. It utilizes the HTTP `POST` request method to create a new resource on Vimeo.
#### Request Parameters

This endpoint takes four body parameters -- let's see them in the table below:

| **Parameter Name** | **Type** | **Category** | **Description**                                                                                                                                                                                                                                                    |
| ------------------ | -------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `description`      | String   | Optional     | This parameter specifies the channel's description. In other words, it explains what the channel is all about.                                                                                                                                                     |
| `link`             | String   | Optional     | This parameter can be used to define a custom link to the channel. The string given to this field will come in place of channel ID. Instead of accessing the channel using a numeric ID (hard to remember); we can use this custom name in the URL.                |
| `name`             | String   | Required     | This field defines the name of a channel.                                                                                                                                                                                                                          |
| `privacy`          | String   | Required     | Here, the privacy level of the channel is specified. <br>`anybody` - anyone can access this channel.<br>`moderators` - only the users who are moderators of this channel can access it.<br>`user` - only the moderators and selected users can access the channel. |
The successful execution of the code below automatically extracts the channel ID and assigns it to the `NEW_CHANNEL_ID`. Click the "save" button to use it in the next sections. Now, click the "RUN" button in the code widget below to create a new channel.

```python
url = "https://api.vimeo.com/channels" 

payload = json.dumps({
    'name': 'Vimeo API Testing Channel',
    'privacy': 'anybody'
})

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer f2ff07be7a2e70828fe9079517c1633b'
    }

response = requests.request("POST", url, headers=headers, data=payload)
if response.status_code != 200:
    print("Following error is produced")
    print(json.dumps(response.json(), indent=4))
else:
    print(json.dumps(response.json(), indent=4))
```

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** We define the `url` that we’ll use later in the code to create a new channel.
- **Lines 3–6:** We define a `payload` object that contains `name` and `privacy` parameters. For this call, we’ve used only two parameters—the remaining two will be used in the next section where we'll edit the channel.
- **Lines 13 and 18:** These lines make a `POST` request and print the response, respectively.
#### Response Fields

Let's have a look at some important response fields returned by the above code in the table below:

| **Field**          | **Description**                                                                                                                                                     |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `uri`          | A string type field that specifies the unique resource identifer for the created channel. The numeric value written at the end of this value is the channel ID. |
| `name`         | This field returns the display name of the channel.                                                                                                             |
| `description`  | This field briefly describes what this channel is all about. Currently, it is `null`.                                                                           |
| `privacy`      | An object that defines the privacy settings of the channel.                                                                                                     |
| `privacy.view` | This field shows the privacy level that we've defined in the call as a parameter.                                                                               |
Let's access our new created channel in the browser.

Use the link given in the response against the `uri` field and append it to '**https://vimeo.com**'. Now hit this complete URL in the browser, and you'll see your new channel. 
### Edit a Channel

In this section, we'll edit the channel we created in the last section. We'll use the unique ID of the channel to access the resource (channel) to make changes to it. We'll use the `{base_url}/channels/{NEW_CHANNEL_ID}` endpoint to achieve this functionality. This endpoint utilizes the HTTP `PATCH` method to edit a channel.
#### Request Parameters

This endpoint takes one required path parameter, `NEW_CHANNEL_ID`, and four optional body parameters -- `description`, `link`, `name` and `privacy`. In the previous section, `name` and `privacy` were the required parameters, but for this endpoint they are optional. 

Let's edit a channel in the code below. We'll use the `description` and `link` parameters to make edits to the channel. The description of the channel is already added in the code widget below but we'll also add a placeholder, `{custom_link}`, for the `link` parameter. Replace this placeholder with a custom or unique link of your choice.

```python
url = "https://api.vimeo.com/channels/{{NEW_CHANNEL_ID}}" 

payload = json.dumps({
    'description': 'This is a demo Channel that we created for API testing......',
    'link': '{custom_link}'
})

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92a0c79ae7e14421c50ae9b017c93a4b2e072209'
    }

response = requests.request("PATCH", url, headers=headers, data=payload)
if response.status_code != 200:
    print("Following error is produced")
    print(json.dumps(response.json(), indent=4))
else:
    print(json.dumps(response.json(), indent=4))
```

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** We define the endpoint for this operation.
- **Lines 3–6:** We add a payload object that includes a `description` and `link` as parameters.
- **Lines 13 and 18:** We create a `PATCH` request, and then print the response, respectively.

### Response

In response to the above code, we can see that the `description` and `link` fields have been updated.
## Manage Channel Categories

Learn how to perform different category operations on a channel using the Vimeo API.
### Overview

In this lesson, we'll learn:

- How to add a channel to a specific category.
- How to get all the categories to which a specific channel belongs.
- How to remove a channel from a category.

We'll use the following endpoints to perform those operations:

- We'll use the `{base_url}/channels/{NEW_CHANNEL_ID}/categories/{category_name}` endpoint to add and remove a channel from a specific category. 
- We'll use the `{BASE_URL}/chnnels/{NEW_CHANNEL_ID}/categories` endpoint to get all categories to which a channel belongs. 

> [!NOTE]
> **Note:** The first endpoint requires the specific channel to belong to the authenticated user. 

### Vimeo Categories

First, let's look at some of the Vimeo categories in the table below. You can also refer to [this](https://www.educative.io/collection/page/10370001/5724185443172352/5344697836371968#Get-all-categories) endpoint to get a list of all the categories.

| **Category name**   | **URL**                         |
| ------------------- | ------------------------------- |
| Ads and Commercials | `/categories/adsandcommercials` |
| Animation           | `/categories/animation`         |
| Branded Content     | `/categories/brandedcontent`    |
| Comedy              | `/categories/comedy`            |
| Documentary         | `/categories/documentary`       |
We'll add our channel in some of these categories in the next section.
### Add a Channel to a Specific Category

This section will add our channel to two Vimeo categories defined in the above table. We'll make two calls to the `channels/{NEW_CHANNEL_ID}/categories/{category_name}` endpoint, each with a different `category_name`. Here, we'll add our channel to the `brandedcontent` and `adsandcommericals` categories.
#### Request Parameters

This endpoint *doesn't take body parameters*, but it does take two required path parameters -- `NEW_CHANNEL_ID` and `category_name`. Let's see the endpoint in the widget below:

```python
url = "https://api.vimeo.com/channels/1927442/categories/brandedcontent"
# url = "https://api.vimeo.com/channels/1927442/categories/adsandcommercials"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
    }

response = requests.request("PUT", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced")
    print(json.dumps(response.json()['developer_message'], indent=4))
else:
    print(response)
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Lines 1 and 2**: We define the URLs to make an API call. The first one is for the `brandedcontent` category and the second one is for `adsandcommericals`. By default, the URL in **line 1** is called, but once it is executed, uncomment **line 2**, comment out **line 1**, and execute the code again. 
- **Lines 9 and 14**: We define the HTTP `PUT` Request method, and the print statement for the response, respectively. You might notice the change in the format of the print statement. 
	- This is because of the fact that this endpoint only gives HTTP code to specify the output of the action.

#### Response

The response of the above code will give an HTTP status code. If the call is successful, then the `204` status is returned. Otherwise, the `4xx` status is returned. Please see the description of the error codes in the appendix section.
### Get All Categories to Which a Channel Belongs

In this section, we'll use the `channels/{NEW_CHANNEL_ID}/categories` endpoint to list all the categories to which a channel belongs.
#### Request Parameters

This endpoint utilizes `GET` method and therefore does not take body parameters, but a required parameter, `NEW_CHANNEL_ID` is passed by including it in the `url` of the request (path parameter). Let's see the working of this endpoint in the code widget below:

```python
url = "https://api.vimeo.com/channels/1927442/categories" 

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")
    
print(json.dumps(response.json(), indent=4))
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: it specifies the `url` for this call that includes `NEW_CHANNEL_ID` as a path parameter
- **Line 8**: It makes a `GET` request to the `url`.
- **Line 12**: It prints the response. 
#### Response Fields

The successful execution of the above code returns two main fields - `total` and `data`. The `total` response field shows the count of the categories to which the specified channel belongs (currently, we have subscribed our channel to two categories). We've already discussed all the important fields from the `data` array in the previous lessons. 
### Remove a Channel From a Category

This section helps us go through the process of channel removal from a category. The removal of a channel from a category uses the same endpoint that was used to add a channel to a specific category, but this time, it uses the HTTP `DELETE` method. 
#### Request Parameters

This endpoint takes two required path parameters, which are `NEW_CHANNEL_ID` and `category_name`.

Let's remove the channel from a specified category in the code below:

```python
url = "https://api.vimeo.com/channels/1927442/categories/brandedcontent" 

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
    }

response = requests.request("DELETE", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced")
    print(json.dumps(response.json(), indent=4), "Response code", response)
else:
    print(response)
```

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** We define the `url` of the request to remove the specified channel ID from the category `brandedcontent`.
- **Line 8:** We make the `DELETE` request to the `url`.
- **Line 13:** We print the response.
#### Response

The response of the above code returns an HTTP status code. A successful call returns the `204` status. Otherwise, the `4xx` status is returned. Please see the description of possible error codes in the appendix [lesson](https://www.educative.io/courses/vimeo-api-python/http-codes-description).
## Manage Channel Subscriptions

Learn how to manage subscriptions and subscribers of a channel using the Vimeo API.
### Overview

This lesson covers subscriptions and subscribers of a channel. We'll perform the following operations:

- Check if a user has subscribed to a channel.
- Make a user subscribe to a specific channel
- Get all the subscribers of a channel.
- Make a user unsubscribe from a specific channel.

> We'll use two endpoints below to achieve these tasks:

- We'll use the `{base_url}/users/{user_id}/channels/{channel_id}` endpoint to check the subscription of any Vimeo user for a channel. We'll also check if we are subscribing to a channel.
- We'll use the `{base_url}/channels/{channel_id}/users` endpoint to get all subscribers of a channel.
### Check if a User has Subscribed to a Channel

In this section, we'll see how to check the subscription status of a specific user for a specific channel. We'll use the `{base_url}/users/{user_id}/channels/{channel_id}` endpoint to check the subscription of any Vimeo user for a channel. We'll also check if we are subscribing to a channel. 
#### Test the Subscription of Channels and Users

We have some channel names with their respective owner (user ID) in the table below. More details about channels in a category and their information is found in this lesson. We can use these values to check the functionality of this endpoint.

| **Channel Id** | **Channel name**                          | **User Id** |
| -------------- | ----------------------------------------- | ----------- |
| 1403294        | Blackmagic Pocket Cinema Camera 4K/6K/Pro | 1867528     |
| 525124         | Fabulous Commercials +++ Plus             | 14520072    |
| 143484         | Francesco Calabrese                       | 1163729     |
We can use these channel IDs and user IDs in the code widget below to check the subscription status. 
#### Request Parameters

This endpoint doesn't take any parameters in the `payload` object. However, it takes two required path parameters -- `user_id` and `channel_id`. Let's check the subscription status in the code widget below.

```python
url = "https://api.vimeo.com/users/1867528/channels/1403294"
# url = "https://api.vimeo.com/me/channels/{{channel_id}}"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803' 
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced")
    print(json.dumps(response.json(), indent=4))
else:
    print(response)
```

> Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: Shows the endpoint for this call. It has two placeholders, `{user_id}` and `{channel_id}`. Replace these placeholders with the values of the first row from the above table and execute the code. 
- **Line 2**: This `url` is to check if we're subscribing to a specific channel. In this case, we only replace the `{channel_id}` placeholder.
- **Lines 9 and 14**: We make a `GET` request to `url`, and print the response code, respectively.
#### Response

The response of the above code gives and HTTP status code. A successful call returns a `204` status; otherwise, the `4xx` status is returned. Please see the description of possible error codes in the appendix lesson.
### Make a User Subscribe to a Specific Channel

This section walks us through the process of subscribing to a specific channel. We'll use the same endpoint as the previous section, `{base_url}/users/{user_id}/channels/{channel_id}`, but this time use the HTTP `PUT` method.
#### Request Parameters

This request takes only two required parameters, `user_id` and `channel_id`, and passes them through the request URL. The code below shows the subscription call to a specific channel.

```python
url = "https://api.vimeo.com/users/222656854/channels/1403294"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803' 
    }

response = requests.request("PUT", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced", "Response code: ", response)
    print(json.dumps(response.json(), indent=4))
else:
    print(response)
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1:** Shows the URL for the channel's subscription call. This `url` contains our ID in place `user_id`. We replace this `{channel_id}` placeholder with the first channel ID from the table above. This `url` subscribes the user to the specified channel.
- **Lines 8 and 13:** We make a `PUT` request to `url`, and print the response code, respectively.
#### Response

 The response of the above code gives an HTTP status code. If the call is successful, the `204` status is returned; otherwise, the `4xx` status is returned. Please see the description of possible error codes in the appendix lesson.

**Note**: Please go back to the first section with the details you used to subscribe to a channel and execute the code again. This time you should get status code `204`. 
### Get All the Subscribers of a Channel

In this section, we'll see how to use the `{base_url}/channels/{channel_id}/users` endpoint to get all the subscribers of a channel.
#### Request Parameters

This endpoint takes path and query parameters. Some important parameters have already been discussed in previous lessons. Let's see some of them in the table below:

| Parameter Name | Type   | Category                   | Description                                                                                        |
| -------------- | ------ | -------------------------- | -------------------------------------------------------------------------------------------------- |
| `channel_id`   | Int    | Required (Path parameter)  | This is a unique ID of the channel for which we want to get all the subscribers                    |
| `direction`    | String | Optional (Path parameter)  | This field specifies the sorting direction of the result.                                          |
| `filter`       | String | Required (Query parameter) | This field specifies the property on which we want to filter the field. Its value is `moderators`. |
| `page`         | Int    | Optional (Query parameter) | Here, we define the page number that we want to get in the result.                                 |
| `per_page`     | Int    | Optional (Query parameter) | This field showws how many results instances we want on a single page.                             |
| `query`        | String | Optional (Query parameter) | If we want to search for a specific search, this field is used.                                    |
| `sort`         | String | Optional (Query parameter) |  There are two methods to sort the results. One is `alphabetical` and the second is `date`.        |
> We'll use `1403294` as a `channel_id` and sort the results based on the `date`. Let's see the code below.

```python
url = "https://api.vimeo.com/channels/1403294/users?sort=date"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803' 
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")

print(json.dumps(response.json(), indent=4))
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: Defines the `url` of the request. We use a test channel ID from the table given in the last section and assign `date` to the `sort` query parameter.
- **Lines 8 and 12**: We make a `GET` request to `url` and print the response, respectively.
#### Response

The successful execution of the above code returns a couple of fields and we've already seen them. If we notice the `data` array in the response, we get our details at the first index of the array.
### Make a User Unsubscribe from a Specific Channel

Let's perform the unsubscription operation on the specified channel. This endpoint requires only two path parameters--`channel_id` and `user_id`

```python
url = "https://api.vimeo.com/users/222656854/channels/1403294"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803' 
    }

response = requests.request("DELETE", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced", "Response code: ", response)
    print(json.dumps(response.json(), indent=4))
else:
    print(response)
```

The above code utilizes the HTTP `DELETE` request to make the user unsubscribe to the channel that they subscribed to in the previous section. The response of the above code gives an HTTP status code. A successful call returns the `204` status; otherwise, the `4xx` status is returned. Please see the description of possible error codes in the [appendix](https://www.educative.io/courses/vimeo-api-python/http-codes-description) lesson.
## Manage Channel Tags

Learn how to perform different operations to manage tags of a channel using the Vimeo API.
### Overview

In this lesson, we'll perform the below two operations related to the tags in a channel:

- Add a tag to a channel
- Get all the tags of a channel

These tasks are achieved by the following endpoints:

- We use the `{base_url}/channels/{channel_id}/tags/{tag_word}` endpoint to add a specific tag to a channel.
- We use the `{base_url}/channels/{channel_id}/tags` endpoint to get all tags of a channel.
### Add a Specific Tag to a Channel

In this section, we'll see how we can add a specific tag to a channel using the Vimeo API. We'll make multiple calls to add multiple tags to our channel, specified by the `channel_id`.
#### Request Parameters

This API call takes two required path parameters -- `channel_id` and `tag_word`. For the code snippet shown in the widget below, we'll use the saved `channel_id` for the channel we created earlier. Let's see the functionality in the code widget below:

```python
url = "https://api.vimeo.com/channels/1927442/tags/entertainment"
# url = "https://api.vimeo.com/channels/1927442/tags/fun"
# url = "https://api.vimeo.com/channels/1927442/tags/games"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
}

response = requests.request("PUT", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced", "Response code: ", response)
```

Let's look at the highlighted lines in the code widget shown above:

- **Lines 1-3**: These lines show the `url` for this call. We define three different tags for the same channel. comment out **line 2 and 3**; execute **line 1** first then comment it and uncomment the next line (**line 2**) and execute it. 
- **Line 10**: We make a `PUT` request.
- **Line 15**: We print the response. 
#### Response

In the response to the above API call, if the call is successful, then an HTTP code `204` is returned; otherwise `4xx` will be returned.
### Get All Tags of a Channel

In this section, we’ll use the `{base_url}/channels/{channel_id}/tags` endpoint to get all the tags related to a channel. This endpoint takes one required parameter `channel_id` and passes it as a path parameter. Some sample channel IDs are shown in the table below.

| **Channel ID** | **Channel name**                          |
| -------------- | ----------------------------------------- |
| 1403294        | Blackmagic Pocket Cinema Camera 4K/6K/Pro |
| 525124         | Fabulous Commercials +++ Plus             |
| 143484         | Francesco Calabrese                       |
> Let's see the working of the endpoint in the code below:

```python
url = "https://api.vimeo.com/channels/1927442/tags"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
}

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")

print(json.dumps(response.json(), indent=4))
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: shows the `url` for this call. By default, we have the ID of our channel placed in the `url` but you can replace this ID with the channel IDs from the table above and see their tags.
- **Line 8**: We create the `GET` request.
- **Line 12**: We print the response.
#### Response Fields

The table below shows the response fields.

| Field   | Description                                                                       |
| ------- | --------------------------------------------------------------------------------- |
| `total` | This integer-type field shows the total number of tags that exist in the channel. |
| `data`  | An array that contains objects of tag's details.                                  |
### Check and Remove a Tag from a Channel

In this section, we'll see two more operations related to a channel's tag. First, we'll check if a specific tag is added to a channel. Second, we'll remove that tag from the channel. In the previous section, we’ve added some tags to our channel. Now, let's check if the tag is present in the channel and delete it. The following endpoint is used for these operations:

- Use the `{base_url}/channels/{NEW_CHANNEL_ID}/tags/{tag_word}` endpoint to check and delete a tag from a channel.
#### Request Parameters

This endpoint also takes only two required path parameters. The first parameter, `NEW_CHANNEL_ID`, is the unique ID of our created channel. The second parameter, `tag_word`, is a tag that we want to check. To delete a tag from a channel, the requestor must be the owner of that channel. Let's check and remove the `entertainment` tag from our channel in the code below.

```python
url = "https://api.vimeo.com/channels/1927442/tags/entertainment"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
}

response = requests.request("GET", url, headers=headers)
if response.status_code != 204:
    print("Following error is produced in GET request. ", "Response code: ", response)
    print(json.dumps(response.json(), indent=4))
else:
    response = requests.request("DELETE", url, headers=headers)
    if response.status_code != 204:
        print("Following error is produced in DELETE request. ", "Response code: ", response)
        print(json.dumps(response.json(), indent=4))
    else:
        print(response)
```

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** Shows the `url` for this call.
- **Lines 8 and 13:** These are the `GET` and `DELETE` requests, respectively.
- **Line 18:** We print the response in case of successful execution of the `DELETE` method.

#### Response

The successful execution of the code widget above returns an HTTP status code `204`.
# Videos
## Search for Videos

Learn how to search for a video and filter the results using the Vimeo API. 
### Overview

This chapter explains some important operations on videos available on Vimeo. In this lesson, we'll see how to make a search for videos based on a query.

- We use the `{base_url}/videos` endpoint to search for videos.
#### Request Parameters

This endpoint does not take body parameters, but it supports query parameters. Let's have a look at these parameters in the table.

| Parameter Name | Type    | Category | Description                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------------- | ------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `direction`    | String  | Optional | This field defines how to sort the results.<br>`asc` - Ascending order<br>`desc` - Descending order                                                                                                                                                                                                                                                                                                              |
| `filter`       | String  | Optional | This field adds a filter to the results. We can filter videos based on some filters. Some of the possible values are:<br>`categories`: apply filter on the video's categories<br>`duration`: apply filter on the video's duration<br>`minimum_likes`: filter videos by the number of minimum likes<br>`trending`: return trending videos<br>`upload_date`: filter by upload date                                 |
| `links`        | String  | Optional | This parameter defines a list, separated by a comma, of video URLs to find.                                                                                                                                                                                                                                                                                                                                      |
| `page`         | Integer | Optional | This parameter takes the page number that we want to show from the result.                                                                                                                                                                                                                                                                                                                                       |
| `per_page`     | Integer | Optional | This parameter controls the number of items per page. The maximum limit is 100.                                                                                                                                                                                                                                                                                                                                  |
| `query`        | String  | Required | The search query on the basis of which we are searching videos.                                                                                                                                                                                                                                                                                                                                                  |
| `sort`         | String  | Optional | This field lets us specify how we want to sort the results.<br>`alphabetical`: sorts results alphabetically<br>`comments`: sorts the results by the number of comments.<br>`date`: sorts the results by date<br>`duration`: sorts the results by duration<br>`likes`: sort the results by the number of likes<br>`plays`: sort the results by the number of plays.<br>`relevant`: sort the results by relevance. |
| `uris`         | String  | Optional | This parameter takes a list of comma-separated video URIs to find.                                                                                                                                                                                                                                                                                                                                               |
> Let's see the functionality of `{base_url}/videos` in the code widget below:

```python
url = "https://api.vimeo.com/videos?query=math"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
}

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")

print(json.dumps(response.json(), indent=4))
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: Defines the `url` to make this call with the query parameter `query`. We use `math` as a test value here, you can use different queries and see other responses.
- **Line 8 and Line 12**: We make the `GET` request to the `url` and print the response, respectively.
#### Response Fields

The response to the above call returns the `data` array along with some other fields related to pagination. We've already discussed most of the fields of the `data` array, but let's see some of the important fields in the table below:

| **Fields**        | **Description**                                                           |
| ------------- | --------------------------------------------------------------------- |
| `uri`         | The canonical relative URI of the channel.                            |
| `name`        | This field defines the title of the video.                            |
| `description` | This field briefly tells about the content of the video.              |
| `link`        | This is a link to the video. We can access the video using this link. |
#### Filter Trending Videos

We've used the `query` parameter to search a video. Now, let's filter the results using the `filter` parameter. We'll filter the videos based on which are trending.

```python
url = "https://api.vimeo.com/videos?query=math&filter=trending"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
}

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced")

print(json.dumps(response.json(), indent=4))
```

The successful execution of the code above returns trending videos as we fine-tune the output response with the `filter` parameter.
## Get all Videos Related to a Specific Video

Learn how to get all related videos to a video using the Vimeo API.
### Overview

In this lesson, we'll see how to fetch videos related to a specific video. The following endpoint is used to perform this task:

- We use the `{base_url}/videos/{video_id}/videos` endpoint to retrieve videos related to a specific video. 

The `{base_url}/videos/{video_id}/videos` endpoint takes the unique ID of a video as a path parameter and returns videos related to it.
#### Request Parameters

This endpoint requires one path parameter, `video_id`, and some query parameters. Let's see those query parameters in the table below:

| Parameter Name | Type    | Category | Description                                |
| -------------- | ------- | -------- | ------------------------------------------ |
| `filter`       | String  | Optional | This field applies a filter to the results |
| `page`         | Integer | Optional |                                            |
| `per_page`     | Integer | Optional |                                            |
Let's see the functionality the in the below code widget:

```python
url = "https://api.vimeo.com/videos/{{VIDEO_ID}}/videos?filter=related"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
}

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced", "Response code: ", response)

print(json.dumps(response.json(), indent=4))
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: We define a `url` to get all videos related to a video specified by `VIDEO_ID` using a query parameter filter.
- **Line 8**: We make a `GET` request
- **Line 12**: We print the response
#### Response Fields

The successful execution of the above code returns a `data` array and some other fields like `total`, `page`, and `per_page`. We've already covered these important fields in the previous lessons.
# Groups
## Create a Group and Get All Groups

Learn how to create a new group programmatically and get all groups from Vimeo.
### Overview

This chapter teaches some important operations for Vimeo groups. We'll learn what these groups are, how to create a group, and how to use that group for videos. Groups are places like communities where the members can share, discuss, and collaborate on videos according to common interests. We can create our own group or contribute to already available groups.

> [!NOTE]
> **Note**: With Vimeo's basic account, we can create only one group. 

This lesson will teach us how to create a new group and get all groups available on the Vimeo platform. We'll be using the `{base_url}/groups` endpoint to achieve these tasks.
### Create a Group

We can create a Vimeo group using an API call fairly easily. All we have to do is make an HTTP `POST` request to the above endpoint.
#### Request Parameters

This endpoint doesn't take a path or query parameters, but does require two body parameters. Let's see them in the table below.

| Parameter Name | Type   | Category | Description                                     |
| -------------- | ------ | -------- | ----------------------------------------------- |
| `name`         | String | Required | This parameter defines the name of the group.   |
| `description`  | String | Optional | This parameter defines briefly about the group. |
Let's see the code in the widget below. It automatically extracts the group ID in the widget after the response. Click the "Save" button to use it in the next lesson(s).

```python
url = "https://api.vimeo.com/groups" 

payload = json.dumps({
    'description': 'This group has been created for demo purpose using API',
    'name': 'Demo API Group'
})

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803' 
}

response = requests.request("POST", url, headers=headers, data=payload)
if response.status_code != 200:
    print("Following error is produced")
    print(json.dumps(response.json(), indent=4), "Response code: ", response)
else:
    print(json.dumps(response.json(), indent=4))
```

Let's have a look at the highlighted lines in the code widget shown above:

- **Line 1**: Defines the `url` that is used later in the code.
- **Line 3-6**: We define a `payload` object that contains `description` and `name` parameters.
- **Line 13**: We make a `POST` request to the `url` defined in line 1.
- **Line 18**: We print the response.
#### Response

The above code returns the metadata about the created group.
### Get All Groups

Now we'll learn how to get all the groups available on the Vimeo platform. This operation utilizes the same endpoint as in the previous section. The only difference is the HTTP request method. 
#### Request Parameters

For this operation, the `{base_url}/groups` endpoint doesn't take path or body parameters -- it takes only query parameters. A list of query parameters, as well as their type, category, and description are given in the table.

| **Parameter Name** | **Type**    | **Category** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------- | ------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `direction`    | String  | Optional | This parameter defines the sorting direction of the results. Its value can either be `asc` or `desc`                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `filter`       | String  | Optional | This parameter is used to apply filter to the groups.<br>`featured` of we want to get only featured groups then this parameter comes in handy.                                                                                                                                                                                                                                                                                                                                                                                         |
| `page`         | Integer | Optional | This parameter defines the page number of the results we want to show.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `per_page`     | Integer | Optional | This parameter defines the number of records to show on a single page. The maximum limit to show items per page is 100.                                                                                                                                                                                                                                                                                                                                                                                                                |
| `query`        | String  | Optional | In this parameter, we can give a search query and the results will be filtered out based on this query.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `sort`         | String  | Optional | This parameter defines the sorting criteria of the results.<br>`alphabetical`: the results will be stored in alphabetical order.<br>`date`: this sorts the results in according to their creation date.<br>`followers`: sorts according to the number of followers<br>`relevant`: this value sorts the results by considering the relevance to the `query` parameter. This means that this value is available only if the `query` parameter is used.<br>`videos`: this sorts the results according to the number of videos in a group. |
Let's see the functionality of this endpoint in the code widget below.

```python
url = "https://api.vimeo.com/groups?&query=fun&sort=date&page=2" 

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803' 
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced", "Response code: ", response)

print(json.dumps(response.json(), indent=4))
```

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** Shows the `url` for this operation. We use three query parameters—the first is `query=fun`, the second is the sorting criteria `sort=date`, and the third is page number `page=2` to show the results.
- **Line 8:** We make the `GET` request to the `url`.
- **Line 12:** We print the response.

### Response Fields

The successful execution of the above code returns a `data` array and some other fields like `total`, `page`, `per_page`. We’ve covered these fields in previous lessons.
## Videos Operations on Vimeo Groups

Learn how to perform different video operations on groups using Vimeo API.
### Overview

In this lesson, we'll see some important operations for the management of videos in groups. We'll learn to add a video to our group and retrieve all the videos form a group. See the endpoints below:

- We'll use the `{base_url}/groups/{GROUP_ID}/videos/{VIDEO_ID}` endpoint to add a video to a group. 
- We'll use the `{base_url}/groups/{GROUP_ID}/videos` endpoint to get all videos from the Vimeo group. 
### Add a Video to a Group

This section teaches us how to add a specific video to a group. The authenticated user must be the owner of the group. We'll add Vimeo videos to our group. A few sample video IDs are given in the table below:

| **Video ID** | **Video Name**                                                |
| ------------ | ------------------------------------------------------------- |
| 391525572    | DIOR - GLITTER                                                |
| 637403296    | Burberry - Open Spaces / Dir. Megaforce                       |
| 397402255    | AirPods Pro - Snap                                            |
| 199930036    | adidas Originals \| 'Original is never finished' \| Chapter 1 |
#### Request Parameters

This endpoint takes two required path parameters—`GROUP_ID` and `VIDEO_ID`. Use an ID from the table above in place of `VIDEO_ID`.

```python
url = "https://api.vimeo.com/groups/{{GROUP_ID}}/videos/{{VIDEO_ID}}"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
    }

response = requests.request("PUT", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced", "Response code: ", response)
    print(json.dumps(response.json(), indent=4))
else:
    print(response)
```

Let's look at the highlighted lines in the code widget shown above:

- **Line 1**: Define the `url` for this operation.
- **Line 8**: We make a `PUT` request.
- **Line 13**: We print the response. 
### Get all the Videos in a Group

This section teaches us how to get all the videos from a specific group. The `{base_url}/groups/{GROUP_ID}/videos` endpoint returns all the videos. Here, `GROUP_ID` is the ID of the group for which we want to fetch all the videos.
#### Request Parameters

This endpoint also takes query parameters, which are described in the table below:

| **Parameter name**  | **Type** | **Category** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------- | -------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `direction`         | String   | Optional     | This parameter defines the sorting direction of the results. Its value can either be `asc` or `desc`.                                                                                                                                                                                                                                                                                                                                                             |
| `filter`            | String   | Optional     | This parameter is used to apply filters to the results.<br><br>- `embeddable` - Returns only those videos that are embeddable.                                                                                                                                                                                                                                                                                                                                    |
| `filter_embeddable` | Boolean  | Optional     | If it is `true` then the results are filtered based on embeddable videos otherwise non-embeddable videos are returned. This parameter is required only when the filter is `embeddable`.                                                                                                                                                                                                                                                                           |
| `page`              | Integer  | Optional     | This parameter shows the number of result pages that we want to show.                                                                                                                                                                                                                                                                                                                                                                                             |
| `per_page`          | Integer  | Optional     | The number of records to show on a single page. Maximum limit is 100.                                                                                                                                                                                                                                                                                                                                                                                             |
| `query`             | String   | Optional     | This field defines the search query to filter the results                                                                                                                                                                                                                                                                                                                                                                                                         |
| `sort`              | String   | Optional     | This parameter defines the sorting criteria of the results.<br><br>- `alphabetical` - The results will be sorted alphabetically.<br>- `date` - This value sorts the results by creation date.<br>- `duration` - Perform sorting based on the duration<br>- `likes` - The result will be sorted by the number of likes.<br>- `plays` - Sort the results by the number of plays<br>- `comments` - This value sorts the results according to the number of comments. |
Let's see the working endpoint in the code widget below.

```python
url = "https://api.vimeo.com/groups/{{GROUP_ID}}/videos"

headers = {
    'Content-type': 'application/json',
    'Authorization': 'Bearer 92c1c5c4784de5c2b0a7aa3bfcf6e803'
    }

response = requests.request("GET", url, headers=headers)
if response.status_code != 200:
    print("Following error is produced", "Response code: ", response)
    
print(json.dumps(response.json(), indent=4))
```

Get all the videos available in a Vimeo group

Let’s have a look at the highlighted lines in the code widget shown above:

- **Line 1:** This is the `url` of the endpoint.
- **Line 8:** We make a `GET` request.
- **Line 12:** We print the response.

## Appendix

| **HTTP Status**           | **Explanation**                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 200 – OK                  | - The request is successful.                                                                                                                                                                                                                                                                                                                                                                                                               |
| 202 – Accepted            | - The video is in pending status.                                                                                                                                                                                                                                                                                                                                                                                                          |
| 204 – No Content          | - The channel was added to the category.<br>- This user follows the category.<br>- The tag is added/removed.<br>- The video is added.<br>- The user is following the category.<br>- The user is no longer following the category.                                                                                                                                                                                                          |
| 304 – Not Modified        | - No videos have been added to the group since the given `If-Modified-Since` header.                                                                                                                                                                                                                                                                                                                                                       |
| 400 – Bad Request         | - A parameter or a tag is invalid.<br>- Error code 2204: The user exceeds the maximum number of channel categories.<br>- Error code 2501: The channel can't have more than 20 tags.<br>- No such tag or channel exists.<br>- Error code 2101: Either the `uris` or `links` parameter has filtering or sorting arguments.<br>- Error code 2204: A problem occurred with the batch request.<br>- The value of the `filter` is not `related`. |
| 401 – Unauthorized        | - Error code 8003: The user credentials are invalid.                                                                                                                                                                                                                                                                                                                                                                                       |
| 403 – Forbidden           | - The requested information is accessible to the authenticated user only.<br>- The authenticated user can't create groups.<br>- The video is already in the group.<br>- The authenticated user can't add videos to the group.<br>- Error code 3200: The authenticated user doesn't own the channel or isn't a channel moderator.<br>- The video can't be added to a channel, or the authenticated user can't add videos to this channel.   |
| 404 – Not Found           | - The specified channel/category/video/group does not exist.<br>- Error code 5000: The tag exists, but the channel isn't tagged by it.                                                                                                                                                                                                                                                                                                     |
| 503 – Service Unavailable | - Search is disabled.<br>- Error code 7300: An internal search error occurred.                                                                                                                                                                                                                                                                                                                                                             |
