---
title: pilotage.spec
---

Name: pilotage
Version: 3.6.6
Release: 1
Summary: Simulation of monitoring on the server
License: LGPL
URL: http://w3.ibm.com/connections/wikis/home?lang=en#/wiki/Pilotage+project
Source: /mnt/ibm/project/pilotage/pilotage-%{version}.tgz
Buildroot: %{_tmppath}/%{name}-%{version}-%{release}
Packager: Tomas Lipensky <tomas.lipensky@cz.ibm.com>

#%define __find_requires %{nil}
#%define __find_depends %{nil}
#%define __os_install_post %{nil}
#%define _enable_debug_packages %{nil}
#%define debug_package %{nil}

%description
Pilotage from Pilotage project is a tool to simulate the monitoring localy on the server. It reads configuration files from BMC Patrol, DM, ITMv5 and ITMv6 and checks the processes and FS on the server. It chacks also URL's and can control Maintenance flag.

%prep
cd /mnt/ibm/projects/pilotage/
tar czvf /mnt/ibm/projects/pilotage/pilotage-%{version}.tgz pilotage-%{version}/*
cp /mnt/ibm/projects/pilotage/pilotage-%{version}.tgz /home/ibm02wrd/rpmbuild/SOURCES
%setup
%build
%install
mkdir -p %{buildroot}/%{_datadir}/%{name}
rm -rf $RPM_BUILD_ROOT
mkdir -p $RPM_BUILD_ROOT/usr/local/exploit/check
install -m 755 pilotage $RPM_BUILD_ROOT/usr/local/exploit/check/pilotage-%{version}
mkdir -p $RPM_BUILD_ROOT/usr/local/man/man1
install -m 644 pilotage.1 $RPM_BUILD_ROOT/usr/local/man/man1/pilotage.1
install -m 755 readme.txt $RPM_BUILD_ROOT/usr/local/exploit/check/
%clean
%pre
%post
mkdir -p /exploit/scripts/unix
chmod o+x /exploit/scripts/unix
ln -sf /usr/local/exploit/check/pilotage-%{version} /exploit/scripts/unix/pilotage
%preun
%postun
rm /exploit/scripts/unix/pilotage
%files
/usr/local/exploit/check/pilotage-%{version}
/usr/local/exploit/check/readme.txt
/usr/local/man/man1/pilotage.1
%docdir /usr/local/exploit/check
