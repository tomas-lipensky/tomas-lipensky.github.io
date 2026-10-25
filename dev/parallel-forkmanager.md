# parallel-forkmanager

======Perl - Parallel::Forkmanager======

```
my $pm = new Parallel::ForkManager(50);
$pm->set_max_procs($max_processes);
for(1..100)
  {
      $pm->start and next;
      ## veci, ktere se delaji paralelne
      $pm->finish;
  }
```
