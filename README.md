# Stack Overflow for Teams User Groups (so4t_user_groups)
An API script for Stack Overflow for Teams that adds users to user groups based on the contents of a CSV file.

## Requirements
* An instance of Stack Overflow Enterprise (no support for Business tier yet)
* Python 3.7 or higher ([download](https://www.python.org/downloads/))
* Operating system: Linux, MacOS, or Windows

## Setup

[Download](https://github.com/jklick-so/so4t_user_groups/archive/refs/heads/main.zip) and unpack the contents of this repository

**Installing Dependencies**

* Open a terminal window (or, for Windows, a command prompt)
* Navigate to the directory where you unpacked the files
* Install the dependencies: `pip3 install -r requirements.txt`

**API Authentication**

You'll need an API key and API token. 

For Stack Overflow Enteprise, documentation for creating the key and token can be found within your instance, at this url: `https://[your_site]/api/docs/authentication`

Creating an access token for Stack Overflow Enterpise can sometimes be tricky for people who haven't done it before. Here are some (hopefully) straightforward instructions:
* Go to the page where you created your API key. Take note of the "Client ID" associated with your API key.
* Go to the following URL, replacing the base URL, the `client_id`, and base URL of the `redirect_uri` with your own: `https://YOUR.SO-ENTERPRISE.URL/oauth/dialog?client_id=111&redirect_uri=https://YOUR.SO-ENTERPRISE.URL/oauth/login_success`

* You may be prompted to login to Stack Overflow Enterprise, if you're not already. Either way, you'll be redirected to a page that simply says "Authorizing Application"
* In the URL of that page, you'll find your access token. Example: `https://YOUR.SO-ENTERPRISE.URL/oauth/login_success#access_token=YOUR_TOKEN`

**Populate the CSV template**

In the [Templates folder](https://github.com/jklick-so/so4t_user_groups/tree/main/Templates), you'll find a CSV file called `users.csv`. This is the file you'll use to indicate which users you wanted added to which user groups. 

There are two columns in the CSV:
* `user_email_or_id` - the unique identifier for the user that you want to assign to a user group. You can use either the user's email addrees or Stack Overflow for Teams user ID. If neither the email address nor the user ID exist in your Stack Overflow for Teams database, the script will skip that row and notify you via the terminal window.
* `group_name_or_id` - the unique identifier for the user group that you want to assign to the user. You can use either a group name or group ID. If you use a name that doesn't exist, the script will create a new user group with that name.

Only a single user and group can be added per line. If you'd like to add multiple users to a single group, you'll need to create a separate line for each user. Likewise, if you'd like to add a single user to multiple groups, you'll need to create a separate line for each group.

## Usage

In a terminal window, navigate to the directory where you unpacked the script. 
Run the script using the following format, replacing the URL, token, and/or key with your own:

`python3 so4t_user_groups.py --url "https://SUBDOMAIN.stackenterprise.co" --key "YOUR_KEY" --token "YOUR_TOKEN" --csv "PATH_TO_CSV"`

The script can take a minute or two to run, particularly as it gathers data via the API. As it runs, it will continue to update the terminal window with the tasks it's performing. When the script completes, it will return you to a command line prompt.

## Support, security, and legal
Disclaimer: the creator of this project works at Stack Overflow, but it is a labor of love that comes with no formal support from Stack Overflow. 

If you run into issues using the script, please [open an issue](https://github.com/jklick-so/so4t_user_groups/issues). You are also welcome to edit the script to suit your needs, steal the code, or do whatever you want with it. It is provided as-is, with no warranty or guarantee of any kind. If the creator wasn't so lazy, there would likely be an MIT license file included.

All data is handled locally on the device from which the script is run. The script does not transmit data to other parties, such as Stack Overflow.
