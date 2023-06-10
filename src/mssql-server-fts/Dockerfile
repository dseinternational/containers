FROM ubuntu:20.04

ENV ACCEPT_EULA=Y
ENV MSSQL_PID=Developer

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -yq curl apt-transport-https gnupg2 && \
    # Get Microsoft repository configuration
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/20.04/mssql-server-2022.list | tee /etc/apt/sources.list.d/mssql-server.list && \
    curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list | tee /etc/apt/sources.list.d/msprod.list && \
    apt-get update && \
    # Install SQL Server
    apt-get install -yq mssql-server && \
    # Install SQL Server Tools
    apt-get install -yq mssql-tools unixodbc-dev && \
    # Install Full Text Search
    apt-get install -yq mssql-server-fts && \
    # Cleanup
    apt-get clean && \
    rm -rf /var/lib/apt/lists

ENTRYPOINT ["/opt/mssql/bin/sqlservr"]

LABEL org.opencontainers.image.source=https://github.com/dseinternational/containers
LABEL org.opencontainers.image.description="Microsoft SQL Server 2022 with Full Text Search on Ubuntu 20.04"
LABEL org.opencontainers.image.licenses=MIT

