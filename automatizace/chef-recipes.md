---
title: Chef - recipes
---

## Odkazy

[Chef](chef.html)  
[Ruby](../dev/ruby.html)  

## Prikazy

include_recipe 'ibm_tsm-client::client-config_linux'  

server_bag = **data_bag_item**('directory', 'file') ... vytvori objekt server_bag z databagu $CHEF/data-bags/directory/file.json  
  variable = server_bag['variable'] ... priradi hodnotu promenne variable z objektu server_bag  
  require 'chef/win32/version'  
  Chef::Application.fatal!('Ouch!!! Bailing out!!!') ... fatal error, vyskoci z behu chef-clienta  
  Chef::ReservedNames::Win32::Version.new  
  Chef::Config['file_cache_path']  
  Chef::Config[:file_cache_path] ... Cache adresar  
  Chef::Log.info(node["ad"]["ou_name"])  
  Chef::Log.error("It is")  
  Chef::Log.debug(url)  
  cookbook_name.delete('_').delete('-')  
  recipe_name.delete('_').delete('-')  
  Time.now  
  Time.utc(*buildDate.to_a)  
  createFile("#{fileLocation}", "#{messageText}", "#{checkOriginalInstallationDate}")  
  registry_get_values('HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters')  

## Promenne

#{recipe_name}  
#{cookbook_name}  
#{**FILE**} ... jmeno aktualniho rubi skriptu  
"#{Chef::Config['file_cache_path']} ... docasny adresar (nastaveny v client.rb)  

tnode=Chef::Node.load(node.name)  
  tnode.run_list &lt;&lt; "role[aaa]" ... prida roli do node  
  tnode.override["ad"]["domain_name"]='aaa'  
  this_node.normal_attrs["ad"]["domain_name"]  
  tnode.save  

## Zdroje - Resorces

[registry_key](https://docs.chef.io/resource_registry_key.html) ... memeni windows registru

```chef
ohai 'reload' do
  action :reload
end
```

```
windows_package "aaa aaa" do
  package_name "aaa aaa"
  source "url/aaa.msi"
  action :install
  source_codes [0, 4, 127, 1]
end
```

```
remote_file "#{localfilepath}" do
  source "#{url}"
  action :create_if_missing
end
```

```
windows_batch 'unzip_tsm_images' do
  code &lt;&lt;-EOH
  "C:\\Program Files\\7-Zip\\7z.exe" x #{localfilepath}  -oC:\\ -r -y
  EOH
  not_if {::File.exists?('C:/tsm_images')}
end
```

```
windows_path 'C:\Perl64\bin' do
  action :add
end
```

```
execute 'create_ico_folder' do
  command 'mkdir /tmp/ico'
  not_if { File.exists?("/tmp/ico") }
end
```

```
bash 'set file permissions' do
  cwd '/tmp/ico/backup_deploy'
  code &lt;&lt;-EOF
    unzip #{localfilepath} -d /tmp/ico
    chmod +x /tmp/ico/backup_deploy/sco_clilnx.sh
    touch /tmp/ico/backup_deploy/sco_clilnx.conf
    chmod 400 /tmp/ico/backup_deploy/sco_clilnx.conf
    mkdir -p /busapps/rexu/100/_lgi/exploitsm/conf/
  EOF
end
```

```
template "/busapps/rexu/100/_lgi/exploitsm/conf/#{node_name_lower}_rbckeur0" do
  source 'journal_key.erb'
  owner "root"
  group "root"
  mode "0600"
end
```

```
powershell_script 'Run KMS Client' do
        code &lt;&lt;-EOH
        cscript "$env:windir\\system32\\slmgr.vbs" -skms #{node[:kms][:server_name]}:#{node[:kms][:server_port]}
        cscript "$env:windir\\system32\\slmgr.vbs" /ato
        EOH
end
```

```
file "#{arg1}" do
    user "root"
    group "root"
    mode "0444"
    content "#{arg2}#{arg3}"
    puts "OK: #{arg1} timestamp file created"
    not_if do ::File.exists?("#{arg1}") end
    end
```

```
ruby_block 'display build timestamp attribute value' do
    block do
      puts "OK: build timestamp attribute is already set to : #{checkOriginalInstallationDate}, nothing to do."
      end
    action :run
end
```
