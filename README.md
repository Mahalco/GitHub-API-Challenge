# GitHub-API-Challenge!
# Creating webhooks

Learn to build a webhook, choosing the events your webhook will listen for on GitHub and how to set up a server to receive and manage the webhook payload.
https://docs.github.com/en/free-pro-team@latest/developers/webhooks-and-events/creating-webhooks

# Configuring your server to receive payloads
## Step One: Download ngrok
https://ngrok.com/download

ngrok is a Go program, distributed as a single executable file for all major desktop platforms.  This is super rad – no additional frameworks to install or other dependencies.  Grab the version for your development system of choice and simply unzip the file somewhere on your computer.

## Step Two: Write a web application 
The next step is to write a web application that can respond to inbound calls. 

As an example, here’s a tiny Sinatra application, written in Ruby, that will respond to a GET request to “/payload” 

webhooks.rb

"\
require 'sinatra'\
require 'json'\
post '/payload' do\
push = JSON.parse(request.body.read)\
puts "I got some JSON: #{push.inspect}"\
end\
"

To run this Ruby application, you will need to have Ruby and the Sinatra gem installed.  On the Mac, you already have Ruby installed.  To install Sinatra, enter the command “gem install sinatra” in a Terminal window to install the Sinatra web framework.  Windows and Linux will require a little more setup.

To start a local HTTP server running this code, open up a Terminal window and create a file called “app.rb”.  Place the code above in this file and save it.  Run the code in your Terminal window with the command “ruby webhooks.rb”.  You should now have a Ruby web server running on local port 4567

We now need to start ngrok, telling it which port we want to expose to the public Internet. In the Terminal, type ./ngrok 4567 on Linux and Mac, and just ngrok 4567 on Windows. After starting up, you should see something like the following:

  Session Status                online \ 
  Account                       amanmahal (Plan: Free) \
  Version                       2.3.35 \
  Region                        United States (us) \
  Web Interface                 http://127.0.0.1:4040 \
  Forwarding                    http://7bd461818ac4.ngrok.io -> http://localhost:4567 \
  Forwarding                    https://7bd461818ac4.ngrok.io -> http://localhost:4567 


See that URL on the ngrok domain? That’s the brand new home of your local web app on the public Internet. In a browser window, open up https://[your generated ID].ngrok.io/payload – this should display the same XML found at http://localhost:4567/payload – verify this is the case.

Start this server up.

Since we set up our webhook to listen to events dealing with Repositories created, deleted, archived, unarchived, publicized, privatized, edited, renamed, or transferred, go ahead and create a new repository. Once you create it, switch back to your terminal. You should see something like this in your output:

I got some JSON: {"ref"=>"refs/heads/main", "before"=>"995d945c9420fa72c332da2fe8772a8ae8092b4b", "after"=>"22a04c4b3af3fbbf7741004e85cbfd7c5c4bfbd5", "repository"=>{"id"=>310928908, "node_id"=>"MDEwOlJlcG9zaXRvcnkzMTA5Mjg5MDg=", "name"=>"GitHub-API-Challenge", "full_name"=>"Mahalco/GitHub-API-Challenge", "private"=>false, "owner"=>{"name"=>"Mahalco", "email"=>nil, "login"=>"Mahalco", "id"=>74116661, "node_id"=>"MDEyOk9yZ2FuaXphdGlvbjc0MTE2NjYx"...

Success! You've successfully configured your server to listen to webhooks.
