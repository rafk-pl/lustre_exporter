# Manual RPM Package Creation

## Create Directory Structure for RPM Build

Top level directory structure:

`mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}`  

Exporter directory:  

`mkdir -p ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/usr/bin`  
`mkdir -p ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/usr/lib/systemd/system`  
`mkdir -p ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/etc/sysconfig`  
`mkdir -p ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/etc/sudoers.d`  

Copy required files from exporter source directory to RPM exporter directory:  

`cp rpm/prometheus-lustre-exporter.spec ~/rpmbuild/SPECS/`  
`cp lustre_exporter ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/usr/bin/`  
`cp systemd/prometheus-lustre-exporter.service ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/usr/lib/systemd/system/`  
`cp systemd/prometheus-lustre-exporter.options ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/etc/sysconfig/`  
`cp sudoers/prometheus-lustre-exporter ~/rpmbuild/SOURCES/prometheus-lustre-exporter-2.1.4/etc/sudoers.d/`

After setup the RPM top level directory should contain the required files:  

`tree ~/rpmbuild/`  
```
rpmbuild/
├── BUILD
├── BUILDROOT
├── RPMS
├── SOURCES
│   └── prometheus-lustre-exporter-2.1.4
│       ├── etc
│       │   ├── sudoers.d
│       │   │   └── prometheus-lustre-exporter
│       │   └── sysconfig
│       │       └── prometheus-lustre-exporter.options
│       └── usr
│           ├── bin
│           │   └── lustre_exporter
│           └── lib
│               └── systemd
│                   └── system
│                       └── prometheus-lustre-exporter.service
└── SPECS
    └── prometheus-lustre-exporter.spec
```
Create source TAR ball for RPM build:  

`cd ~/rpmbuild/SOURCES; tar -czvf prometheus-lustre-exporter-2.1.4.tar.gz prometheus-lustre-exporter-2.1.4`  

> Use relative path here, otherwise rpmbuild will not find the extracted files.  

Build the RPM package:  

`rpmbuild -ba ~/rpmbuild/SPECS/prometheus-lustre-exporter.spec`  
