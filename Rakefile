desc "Runs cron maintenance tasks."
task :cron do
    #Requires task_output set and CRON_EMAIL env variable set
    puts "Running cron at #{Time.now.strftime('%Y/%m/%d %H:%M:%S')}..."
    task_output = `ls`
    if task_output.length > 0
        require 'net/smtp'
        message = "From: #{ENV['SENDGRID_USERNAME']}\n"
        message += "To: #{ENV['CRON_EMAIL']}\n"
        message += "Subject: Cron\n\n"
        message += task_output
        Net::SMTP.start('smtp.sendgrid.net', 587, 'heroku.com', ENV['SENDGRID_USERNAME'], ENV['SENDGRID_PASSWORD'], :plain) do |smtp|
              smtp.send_message message, ENV['SENDGRID_USERNAME'], [ENV['CRON_EMAIL']]
        end
    end
end
