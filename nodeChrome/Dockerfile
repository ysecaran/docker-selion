FROM selion/node-base:1.0.0
MAINTAINER Selion <selion@googlegroups.com>

USER root

#===============
# Google Chrome
#===============
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
  && apt-get update -qqy \
  && apt-get -qqy install \
    google-chrome-stable \
  && rm /etc/apt/sources.list.d/google-chrome.list \
  && rm -rf /var/lib/apt/lists/*

#==================
# Chrome webdriver
#==================
ENV CHROME_DRIVER_VERSION 2.20
RUN wget --no-verbose -O /tmp/chromedriver_linux64.zip https://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip \
  && rm -rf /opt/selion/chromedriver \
  && unzip /tmp/chromedriver_linux64.zip -d /opt/selion \
  && rm /tmp/chromedriver_linux64.zip

#========================
# Selenium Configuration
#========================
COPY config.json /opt/selion/config.json

# Empty file to suppress downloads
COPY download.json $SELION_HOME/config/download.json

#=================================
# Chrome Launch Script Modication
#=================================
COPY chrome_launcher.sh /opt/google/chrome/google-chrome
RUN chmod +x /opt/google/chrome/google-chrome

RUN chown -R seluser /opt/selion

USER seluser
