FROM ubuntu:18.04
MAINTAINER ali.attari52
RUN apt-get upgrade && apt-get update -y
RUN apt-get install curl jq sendmail -y
RUN curl -H "Content-Type: application/json"  https://api.github.com/repos/nodejs/node/pulls?state=all | jq '.[] | {url,state,title,created_at} | select((.created_at | contains("2022-07"))) | select((.state | contains ("open")))' > /tmp/openrequests.txt
RUN curl -H "Content-Type: application/json"  https://api.github.com/repos/nodejs/node/pulls?state=all | jq '.[] | {url,state,title,created_at} | select((.created_at | contains("2022-07"))) | select((.state | contains ("closed")))' > /tmp/closedrequests.txt
RUN curl -H "Content-Type: application/json"  https://api.github.com/repos/nodejs/node/pulls?state=all | jq '.[] | {url,state,title,created_at} | select((.created_at | contains("2022-07"))) | select((.state | contains ("progess")))' > /tmp/progressrequests.txt
CMD echo "\n\nFROM: Ali\nTO: ALL Users\nSubject:NodeJs Open Pull Requests this month\nBody:\n$(cat /tmp/openrequests.txt)" && echo "\n\nFROM: Ali\nTO: ALL Users\nSubject:NodeJs Closed Pull Requeststhis month\nBody:\n$(cat /tmp/closedrequests.txt)" && echo "\n\nFROM: Ali\nTO: ALL Users\nSubject:NodeJs InProgress Requests this month\nBody:\n$(cat /tmp/progressrequests.txt)"
