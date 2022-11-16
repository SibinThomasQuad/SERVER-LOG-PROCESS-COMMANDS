# SERVER-LOG-PROCESS-COMMANDS

# NGINX
visiting ip adrress in a specific url
    awk -F\" '($2 ~ "/admin/login"){print $1}' access.log | awk '{print $1}' | sort | uniq -c | sort -r

  Most requested urls
              awk -F\" '{print $2}' access.log | awk '{print $2}' | sort | uniq -c | sort -r

  Mostly 404 attempts
              awk '($9 ~ /404/)' access.log | awk -F\" '($2 ~ "^GET .*\.php")' | awk '{print $7}' | sort | uniq -c | sort -r | head -n 20


Most requested url with specific keyword
awk -F\" '($2 ~ ".env"){print $2}' access.log | awk '{print $2}' | sort | uniq -c | sort -r

List of visited ip address in nginx log
sudo awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr


How to parse Nginx access logs for counting requests per second
sudo cat /var/log/nginx/access.log | awk '{print $4}' | uniq -c | sort -rn | head


How to parse Nginx access logs for getting response codes
sudo cat /var/log/nginx/access.log | cut -d '"' -f3 | cut -d ' ' -f2 | sort | uniq -c | sort -rn


List All 301 Permanently Moved URLs
awk '($9 ~ /301/)' /var/log/nginx/access.log | awk '{print $7}' | sort | uniq -c | sort -r | head


We can also check from which source IP you are 404 request are coming .
awk -F\” ‘($2 ~ “/survey/report/na”){print $1}’ looklinix.com_access.log | awk ‘{print $1}’ | sort | uniq -c | sort –r


APACHE

awk '{print $1}' combined_log         # requester ip address (%h)
awk '{print $2}' combined_log         # (%l) (the virtualhost being requested)
awk '{print $3}' combined_log         # userid (%u) (if basic auth was used)
awk '{print $4,5}' combined_log       # date/time (%t)
awk '{print $6}' combined_log         # Request Type (GET, POST, etc..)
awk '{print $7}' combined_log         # URL Requested (/about, or /blog or /xmlrpc.php) etc
awk '{print $8}' combined_log         # HTTP version 

awk '{print $9}' combined_log         # status code (%>s)
awk '{print $10}' combined_log        # size (%b)

awk '{print $11}' combined_log        # http referer 
awk '{print $12}' combined_log        # User Agent

awk -F\" '{print $2}' combined_log    # request line (%r)
awk -F\" '{print $4}' combined_log    # referer
awk -F\" '{print $6}' combined_log    # user agent


Summarize the response codes
awk '{print $9}' combined_log | sort | uniq -c | sort -r       

Find the ips that are causing the most number of 403sPermalink
awk '($9 ~ /403/)' combined_log | awk '{print $1,$7}' | uniq -c | sort -r
