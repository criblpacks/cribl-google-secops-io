# Google Security Operations (SecOps)
----


## About this Pack

This pack is built as a complete SOURCE + DESTINATION solution (identified by the IO suffix). Data collection and delivery happen entirely within the pack's context, eliminating the need to connect it to globally defined Sources and Destinations. This Cribl Pack is designed to streamline the integration of common Cribl data sources with Google Security Operations (SecOps). It provides pre-configured sources, destinations, pipelines, and routes to format and enrich data from various sources, ensuring compatibility with Google SecOps ingestion requirements. The pack simplifies the process of collecting, normalizing, and forwarding security events, enabling efficient analysis and threat detection within the Google SecOps platform.


Key features include:
- Support for common Cribl sources such as Palo Alto Networks Firewall, Cisco ASA, and Windows Event logs.
- Data normalization and enrichment for seamless integration with Google SecOps schemas.
- Optimized routing and filtering to ensure relevant data is sent efficiently.
- Easy-to-customize configurations to adapt to specific use cases or environments.


This pack is ideal for security teams looking to leverage Cribl's data processing capabilities to enhance their Google SecOps workflows.


This pack is meant to include the full workflow from the start and additional sources will be available with updates. A complete list of available sources and their associated log type can be found in Knowledge > lookups > google_secops_source_mapping.csv


## Deployment


Once the pack is installed from the Cribl Dispensary, only a few configurations will need to be modified to start data flowing. Below are the configuration items for each available source and destination. It is recommended that if a source is not to be used that it is disabled in order to prevent unnecessary open port conflicts. For any variables referenced, you can update under Knowledge > Variables within this Pack.


### Destination(s)


#### Google Security Operations
Configuration:
- `GCP project ID` - The Google Cloud Platform (GCP) project ID to send events to
- `GCP Instance` - The Google Cloud Platform (GCP) instance to send events to. This is the Chronicle customer uuid.
- `Namespace` (Optional) - Unique namespace that can be provided to separate data going into Google SecOps

In order to complete configuration for your Google SecOps destination you will need to navigate to the Google Security Operations Pack > Destinations > Google Cloud Chronicle API > cribl-secops. 

1. From General Settings - replace `GCP project ID`, `GCP Instance`, and optionally `Namespace`
2. From Authentication - Ensure the drop down is set to `Service account credentials` and in the large text box, please either upload or paste the full JSON object that contains your Service account credentials provided from Google SecOps.


### Source(s)


#### Palo Alto Networks Firewall


Source: Syslog
Variables:
- `Palo_Alto_Networks_UDP_Port`
- `Palo_Alto_Networks_TCP_Port`


Configure the syslog sender on your Palo Alto Networks appliance to forward to the port specified. The default port is set to `20000` which should be open by default on any Cribl managed cloud worker.


#### Cisco ASA


Source: Syslog
Variables:
- `Cisco_ASA_UDP_Port`
- `Cisco_ASA_TCP_Port`


Configure the syslog sender on your Cisco ASA appliance to forward to the port specified. The default port is set to `20001` which should be open by default on any Cribl managed cloud worker.


#### Fortigate Fortinet Firewall


Source: Syslog
Variables:
- `Fortigate_Firewall_UDP_Port`
- `Fortigate_Firewall_TCP_Port`


Configure the syslog sender on your Fortigate Fortinet appliance to forward to the port specified. The default port is set to `20002` which should be open by default on any Cribl managed cloud worker.


#### Windows Event log


Source: Cribl HTTP (events sourced from Cribl Edge)
Variables:
- `Windows_Event_Log_Port`


This source is designed to receive Windows Event Logs from Cribl Edge. Currently Google Security Operations only accepts Windows Event Logs in the XML format. Please make sure that on your Cribl Edge deployments Windows Event Source they are configured to send as XML.


#### AWS VPC Flowlogs


Source: Amazon Kinesis
Variables:
- `AWS_VPC_Flowlogs_Stream_Name` - Kinesis Data Stream to read data from
- `AWS_VPC_Flowlogs_Region` - Region where the Kinesis stream is located


Amazon Kinesis has multiple authentication methods available for configuration. Please select the proper one through Sources > Amazon Kinesis > AWS_VPC_Flowlogs > Authentication. For more information regarding authentication methods please reference https://docs.cribl.io/stream/sources-kinesis-streams.


## Upgrades

Upgrading certain Cribl Packs using the same Pack ID can have unintended consequences. See [Upgrading an Existing Pack](https://docs.cribl.io/stream/packs#upgrading) for details.


## Release Notes

### Version 1.0.0
- Updated to use the latest Google Cloud Chronicle API Destination

### Version 0.1.0
- Initial release


## Contributing to the Pack


To contribute to the Pack, please connect with us on [Cribl Community Slack](https://cribl-community.slack.com/). You can suggest new features or offer to collaborate.


## License
This Pack uses the following license: [Apache 2.0](https://github.com/criblio/appscope/blob/master/LICENSE).



