# GitHub-API-Challenge!
#Creating webhooks

https://docs.github.com/en/free-pro-team@latest/developers/webhooks-and-events/creating-webhooks

#Configuring your server to receive payloads
##Step One: Download ngrok
ngrok is a Go program, distributed as a single executable file for all major desktop platforms.  This is super rad – no additional frameworks to install or other dependencies.  Grab the version for your development system of choice and simply unzip the file somewhere on your computer.

##Step Two: Write a web application 
The next step is to write a web application that can respond to inbound calls. 

As an example, here’s a tiny Sinatra application, written in Ruby, that will respond to a GET request to “/payload” 

webhooks.rb
"
require 'sinatra'
require 'json'

post '/payload' do
  push = JSON.parse(request.body.read)
  puts "I got some JSON: #{push.inspect}"
end
"
To run this Ruby application, you will need to have Ruby and the Sinatra gem installed.  On the Mac, you already have Ruby installed.  To install Sinatra, enter the command “gem install sinatra” in a Terminal window to install the Sinatra web framework.  Windows and Linux will require a little more setup.

To start a local HTTP server running this code, open up a Terminal window and create a file called “app.rb”.  Place the code above in this file and save it.  Run the code in your Terminal window with the command “ruby webhooks.rb”.  You should now have a Ruby web server running on local port 4567

We now need to start ngrok, telling it which port we want to expose to the public Internet. In the Terminal, type ./ngrok 4567 on Linux and Mac, and just ngrok 4567 on Windows. After starting up, you should see something like the following:
Session Status                online
Account                       amanmahal (Plan: Free)
Version                       2.3.35
Region                        United States (us) 
Web Interface                 http://127.0.0.1:4040 
Forwarding                    http://7bd461818ac4.ngrok.io -> http://localhost:4567
Forwarding                    https://7bd461818ac4.ngrok.io -> http://localhost:4567 

See that URL on the ngrok domain? That’s the brand new home of your local web app on the public Internet. In a browser window, open up https://[your generated ID].ngrok.io/payload – this should display the same XML found at http://localhost:4567/payload – verify this is the case.
