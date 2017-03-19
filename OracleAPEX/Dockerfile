# LICENSE CDDL 1.0 + GPL 2.0
#
# Copyright (c) 1982-2017 Oracle and/or its affiliates. All rights reserved.
#
# ORACLE DOCKERFILES PROJECT
# --------------------------
# This is the Dockerfile for Oracle Database 12c Release 1 Enterprise Edition
# 
# REQUIRED FILES TO BUILD THIS IMAGE
# ----------------------------------
# (1) apex_5.1.zip
#     Download Oracle Database APEX 5.1
#     from http://www.oracle.com/technetwork/developer-tools/apex/downloads/
# (2) ords.3.0.9.348.07.16.zip
#     Download Oracle REST Data Services 3.0.9
#     from http://www.oracle.com/technetwork/developer-tools/rest-data-services/downloads/index.html
#
# HOW TO BUILD THIS IMAGE
# -----------------------
# Put all downloaded files in the same directory as this Dockerfile
# Run: 
#      $ docker build -t oracle/database:12.2.0.1-ee . 
#
# Pull base image
# ---------------
FROM oracle/database:12.2.0.1-se2

# Maintainer
# ----------
MAINTAINER Michael Simons <michael@simons.ac>

# Environment variables required for this build (do NOT change)
# -------------------------------------------------------------
ENV INSTALL_FILE_APEX="apex_5.1.zip" \
    INSTALL_FILE_ORDS="ords.3.0.9.348.07.16.zip" \
    APEX_DIR="apex51"
    SETUP_FILE="setupApex.sh" \
    RUN_FILE_APEX="runOracleWithApex.sh"

# Copy binaries
# -------------
COPY $INSTALL_FILE_APEX $INSTALL_FILE_ORDS $SETUP_FILE $RUN_FILE_APEX $INSTALL_DIR/

# Install JDK and Tomcat for ORDS
USER root
RUN yum -y install java-1.8.0-openjdk tomcat && \ 
    yum clean all && \
    systemctl enable tomcat
    
# Unzip APEX and ORDS files
USER oracle
RUN unzip $INSTALL_DIR/$INSTALL_FILE_APEX -d $ORACLE_BASE/$APEX_DIR && \
    unzip $INSTALL_DIR/$INSTALL_FILE_ORDS -d $ORACLE_BASE/ords