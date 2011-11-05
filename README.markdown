#Heroku Cedar Cron
I've been playing with Heroku and wanted to use the default `cron` addon to run a Python script and only email if that script printed anything to stdout; regular Unix style.

This is my attempt that.

##Usage
The Heroku Cron addon runs `rake cron` once a day and that's about it. By using Ruby's backtick operator, you can run any command command capture the stdout. Then using the Sendgrid addon, you can optionally email that stdout.

You need to edit the Rakefile to enter the task you want to run and set the CRON_EMAIL address,for the script to email you.

There is a requirements.txt file in this repo to trick Heroku into thinking this a Python app. Change that file to whatever your Cedar stack type requires (gem or npm)

##Starting From Scratch
Run these commands to give things a try (assuming you already have the Heroku gem and a Heroku account).

	#create stack
	heroku create --stack cedar

	#push this repo
	git push heroku master

	#add your crontab email addresss
	heroku config:add CRON_EMAIL="email@address.com"

	#add the sendgrid addon
	heroku addons:add sendgrid:starter

	#now run the crontask and you should get an email shortly!
	heroku run rake cron

	#now if you add the crontab addon, that task will be run daily
	heroku addons:add cron:daily