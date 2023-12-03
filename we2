import bs4 as bs
import smtplib
import urllib.request
from email.mime.text import MIMEText

# SCRAPE WEATHER

source = urllib.request.urlopen('https://weather.com/weather/tenday/l/a496cfcba367ffae60ccfdc94e31bcf3d0a12ac6515336dbd274f381a932abbc').read()
soup = bs.BeautifulSoup(source,'html.parser')
asdf = soup.get_text()

asdf2 = asdf[asdf.find('Arrow Up')+8:]
dayofweek = asdf2[:3]
day_weather =  asdf2[asdf2.find('|')+2:asdf2.find('mph')+3]
asdf2 = asdf2[asdf2.find('|')+2:]
asdf2 = asdf2[asdf2.find('|'):]
night_weather = asdf2[asdf2.find('|')+2:asdf2.find('mph')+3]

subject = dayofweek + ': ' + day_weather + ', ' + night_weather

subject = subject.replace('Rain',' Rain ')
subject = subject.replace('Wind',' Wind ')
subject = subject.replace('\xa0','')
subject = subject.replace('Day',' Day ')
subject = subject.replace('Night',' Night ')
subject = subject.replace('°','° ')

subject = subject.replace('  ',' ')

# SEND EMAIL
body = " "
sender = "EMAIL@gmail.com"
recipients = ["EMAIL@gmail.com"]
password = "PASSWORD"

def send_email(subject, body, sender, recipients, password):
    msg = MIMEText(body)
    msg['Subject'] = subject
    msg['From'] = sender
    msg['To'] = ', '.join(recipients)
    with smtplib.SMTP_SSL('smtp.gmail.com', 465) as smtp_server:
        smtp_server.login(sender, password)
        smtp_server.sendmail(sender, recipients, msg.as_string())
    print("Message sent!")


send_email(subject, body, sender, recipients, password)
