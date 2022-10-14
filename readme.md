## Assemblyline 4 - Docker compose documentation

There are two types of configuration possible:
    
- Minimal appliance
- Full Appliance

```NOTE:``` Appliances are built on top of docker but for the moment they do not support Docker in swarm mode.

### Minimal Appliance

This setup includes the bare-minimum components for everything to be able to run. There will be no metrics collected and you will have to tail the log from the docker container logs.

### Full Appliance

This setup includes every single components and all metrics and logging capabilities. Metrics and logs will be gathered inside the same Elasticsearch instance as the processing data and you will have access kibana to view all of those.

## Setup

For full documentation on how to setup an assemblyline appliance see the documentation page. 
https://cybercentrecanada.github.io/assemblyline4_docs/

#### Quickstart

##### 1. Install docker and docker-compose on a linux system
##### 2. Clone this repository

    git clone https://github.com/CybercentreCanada/assemblyline-docker-compose.git

##### 3 Choose deployment type

Choose one of the minimal or full deployments. The rest of the commands 
and paths given will be relative to the directory specific to the deployment
type you are doing. 
    
    cd assemblyline-docker-compose/minimal_appliance

or

    cd assemblyline-docker-compose/full_appliance

##### 4. Copy in an existing or generate a self signed certificate into the `./config` directory in the cloned repository
    
    openssl req -nodes -x509 -newkey rsa:4096 -keyout ./config/nginx.key -out ./config/nginx.crt -days 365 -subj "/C=CA/ST=Ontario/L=Ottawa/O=CCCS/CN=assemblyline.local"
    
##### 5. Set passwords and paths in `./.env` and `./config/bootstrap.py`
##### 6. Launch the system
    
Pull the containers and launch the core system.
    
    sudo docker-compose pull
    sudo docker-compose up -d

Pull the containers and perform first time only setup and install.

    sudo docker-compose -f bootstrap-compose.yaml pull 
    sudo docker-compose -f bootstrap-compose.yaml up -d 
 

 ---

 # installazione assemblyline minimal

git clone https://github.com/CybercentreCanada/assemblyline-docker-compose
cd assemblyline-docker-compose/minimal_appliance/
openssl req -nodes -x509 -newkey rsa:4096 -keyout ./config/ -out ./config/ -days 365 -subj "/C=CA/ST=Ontario/L=Ottawa/O=CCCS/CN=assemblyline.local"

#cd privilege-core-image
#docker build -t privilege-core-image --build-arg "version=latest" .
#cd ..

docker-compose up -d

# only first time
docker-compose -f bootstrap-compose.yaml up -d first_time_setup; docker-compose -f bootstrap-compose.yaml logs -f first_time_setup

# ANALYZER ATTIVATI
docker-compose -f bootstrap-compose.yaml up -d service_configextractor; docker-compose -f bootstrap-compose.yaml logs -f service_configextractor
docker-compose -f bootstrap-compose.yaml up -d service_deobfuscripter; docker-compose -f bootstrap-compose.yaml logs -f service_deobfuscripter
docker-compose -f bootstrap-compose.yaml up -d service_floss; docker-compose -f bootstrap-compose.yaml logs -f service_floss
docker-compose -f bootstrap-compose.yaml up -d service_frankenstrings; docker-compose -f bootstrap-compose.yaml logs -f service_frankenstrings
docker-compose -f bootstrap-compose.yaml up -d service_oletools; docker-compose -f bootstrap-compose.yaml logs -f service_oletools
docker-compose -f bootstrap-compose.yaml up -d service_vipermonkey; docker-compose -f bootstrap-compose.yaml logs -f service_vipermonkey
docker-compose -f bootstrap-compose.yaml up -d service_xlmmacrodeobfuscator; docker-compose -f bootstrap-compose.yaml logs -f service_xlmmacrodeobfuscator
docker-compose -f bootstrap-compose.yaml up -d service_yara; docker-compose -f bootstrap-compose.yaml logs -f service_yara
docker-compose -f bootstrap-compose.yaml up -d service_pefile; docker-compose -f bootstrap-compose.yaml logs -f service_pefile
docker-compose -f bootstrap-compose.yaml up -d service_peepdf; docker-compose -f bootstrap-compose.yaml logs -f service_peepdf
docker-compose -f bootstrap-compose.yaml up -d service_pdfid; docker-compose -f bootstrap-compose.yaml logs -f service_pdfid
docker-compose -f bootstrap-compose.yaml up -d service_pixaxe; docker-compose -f bootstrap-compose.yaml logs -f service_pixaxe
docker-compose -f bootstrap-compose.yaml up -d service_emlparser; docker-compose -f bootstrap-compose.yaml logs -f service_emlparser
docker-compose -f bootstrap-compose.yaml up -d service_characterize; docker-compose -f bootstrap-compose.yaml logs -f service_characterize
docker-compose -f bootstrap-compose.yaml up -d service_extract; docker-compose -f bootstrap-compose.yaml logs -f service_extract
docker-compose -f bootstrap-compose.yaml up -d service_jsjaws; docker-compose -f bootstrap-compose.yaml logs -f service_jsjaws
docker-compose -f bootstrap-compose.yaml up -d service_overpower; docker-compose -f bootstrap-compose.yaml logs -f service_overpower
docker-compose -f bootstrap-compose.yaml up -d service_metapeek; docker-compose -f bootstrap-compose.yaml logs -f service_metapeek
docker-compose -f bootstrap-compose.yaml up -d service_safelist; docker-compose -f bootstrap-compose.yaml logs -f service_safelist
docker-compose -f bootstrap-compose.yaml up -d service_urldownloader; docker-compose -f bootstrap-compose.yaml logs -f service_urldownloader
docker-compose -f bootstrap-compose.yaml up -d service_unpacker; docker-compose -f bootstrap-compose.yaml logs -f service_unpacker
docker-compose -f bootstrap-compose.yaml up -d service_virustotal; docker-compose -f bootstrap-compose.yaml logs -f service_virustotal
docker-compose -f bootstrap-compose.yaml up -d service_sigma; docker-compose -f bootstrap-compose.yaml logs -f service_sigma
docker-compose -f bootstrap-compose.yaml up -d service_antivirus; docker-compose -f bootstrap-compose.yaml logs -f service_antivirus

# ANALYZER NON ATTIVATI
#docker-compose -f bootstrap-compose.yaml up -d service_cuckoo; docker-compose -f bootstrap-compose.yaml logs -f service_cuckoo
#docker-compose -f bootstrap-compose.yaml up -d service_suricata; docker-compose -f bootstrap-compose.yaml logs -f service_suricata
#docker-compose -f bootstrap-compose.yaml up -d service_torrentslicer; docker-compose -f bootstrap-compose.yaml logs -f service_torrentslicer
#docker-compose -f bootstrap-compose.yaml up -d service_beaver; docker-compose -f bootstrap-compose.yaml logs -f service_beaver
#docker-compose -f bootstrap-compose.yaml up -d service_espresso; docker-compose -f bootstrap-compose.yaml logs -f service_espresso
#docker-compose -f bootstrap-compose.yaml up -d service_apkaye; docker-compose -f bootstrap-compose.yaml logs -f service_apkaye
#docker-compose -f bootstrap-compose.yaml up -d service_iparse; docker-compose -f bootstrap-compose.yaml logs -f service_iparse
#docker-compose -f bootstrap-compose.yaml up -d service_tagcheck; docker-compose -f bootstrap-compose.yaml logs -f service_tagcheck
#docker-compose -f bootstrap-compose.yaml up -d service_metadefender; docker-compose -f bootstrap-compose.yaml logs -f service_metadefender
#docker-compose -f bootstrap-compose.yaml up -d service_swiffer; docker-compose -f bootstrap-compose.yaml logs -f service_swiffer
#docker-compose -f bootstrap-compose.yaml up -d service_unpacme; docker-compose -f bootstrap-compose.yaml logs -f service_unpacme