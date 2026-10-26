---
title: Perl - IO::Socket
---

use IO::Socket;  
$remote = IO::Socket::INET->new( Proto     => "tcp", PeerAddr  => $host, Timeout => "5", PeerPort  => "http(80)" );  
unless ($remote) { die "cannot connect to http daemon on $host" }  
        $remote->autoflush(1);  
        print $remote "GET $document HTTP/1.0\n\n";  
        while ( <$remote> ) { print }  
        close $remote;
