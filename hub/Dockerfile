FROM selion/base:1.0.0
MAINTAINER Selion <selion@googlegroups.com>

EXPOSE 4444

ENV SELION_HOME /opt/selion

# SeLion hub Configuration
ENV GRID_NEW_SESSION_WAIT_TIMEOUT 600000
ENV GRID_JETTY_MAX_THREADS 1000
ENV GRID_NODE_POLLING  5000
ENV GRID_CLEAN_UP_CYCLE 5000
ENV GRID_TIMEOUT 30000
ENV GRID_BROWSER_TIMEOUT 180000
ENV GRID_MAX_SESSION 5
ENV GRID_UNREGISTER_IF_STILL_DOWN_AFTER 30000

COPY generate_config /opt/selion/generate_config
RUN chmod 755 /opt/selion/generate_config

# SeLionConfig configuration
ENV SELGRID_RESTART_CYCLE 60000
ENV SELGRID_UNIQUE_SESSION_COUNT 50
ENV SELGRID_NODE_RECYCLE_THREAD_TIMEOUT 1200
ENV SELGRID_NODE_AUTH "authorized"

COPY generate_selionConfig /opt/selion/generate_selionConfig
RUN chmod 755 /opt/selion/generate_selionConfig

# Empty file to suppress downloads
COPY download.json $SELION_HOME/config/download.json

COPY entry_point.sh /opt/selion/entry_point.sh

RUN chown -R seluser /opt/selion
RUN chmod 755 /opt/selion/entry_point.sh

USER seluser

CMD ["/opt/selion/entry_point.sh"]
