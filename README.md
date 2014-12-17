# AIX Errpt Log Content Pack for IBM Smart Cloud Analytics Log Analysis (SCALA)

# What's Included?

1 - A sample logstash configuration **(aixerrpt-example.conf)**
2 - A logstash grok pattern for aixerrpt log messages **(AIXERRPT)**
3 - A SCALA DSV Pack properties file **(aixerrpt.props)**
4 - A sample AIX Errpt logfile **(aixerrpt-sample.log)**

# Deploying the Content Pack

1. Review the sample logstash configuration **(aixerrpt-example.conf)** and determine how you will use the inputs, filters and outputs.  You can use this example or just copy the needed parts into your main logstash configuration file.

2. Determine how you will bring your logs in (eg LFA, file import, etc.) and update the input section appropriately.

3. Review the filters section and determine if any changes are needed based upon how you use logstash, which version you use, etc.

4. Review the output section and update based on your current logstash integration with SCALA. This example configuration will only work with the upcoming release of the SCALA-Logstash Integration.  If you do not have this, contact Doug McClure for assistance.

5. Place the logstash GROK pattern file **(AIXERRPT)** into the appropriate location.  If you are using logstash 1.4.2, you may place this into the /patterns directory and you'll be all set. If you are using logstash 1.5 beta, you can place it into the same /patterns directory, but you will need to use the patterns_dir setting to this location in each filter using the GROK patterns (eg multiline, grok).

6. Copy the DSV Pack properties file **(aixerrpt.props)** into the $SCALAHOME/unity_content/DSVToolkit_v1.1.0.2 directory.

7. Edit the aixerrpt.props file and update the scalaHome directory path.  You may also want to optimize the various index configuration fields in this file. For example, setting filterable = false for the SEQUENCENUMBER field if you don't feel faceting on SEQUENCENUMBER would be useful.

8. Execute this command to build and deploy the DSV Content Pack into SCALA: **python dsvGen.py aixerrpt.props -d -f -u unityadmin -p unityadmin**

9. Create a SCALA datasource which uses the new DSV Content Pack named **aixerrpt**. Be sure to set the host and path values to match what you're setting in your logstash configuration. By default, they are **host = aixerrpt and path = aixerrpt**.

10. Start up logstash and stream your AIX Errpt logs into SCALA and verify you see data in your search results.

# Need Help?

This is a community contributed content pack and no explicit support, guarantee or warranties are provided by IBM nor the contributor. Feel free to engage the community on the ITOAdev forum if you need help!