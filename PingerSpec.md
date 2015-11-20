# Introduction #

The lan-crawler project needs a simple pinger, it's implementation details are described here.

# Overview #

## Goal ##

The end result is to have a maximally up-to-date list of LAN machines that are currently online.

## Logical walkthrough ##

The pinger is largely parallelized, and consists of these logical steps:

  1. Create a list of machines to ping given the IP Ranges of interest
  1. Schedule ping tasks to an executing schedule pool
  1. Save the current ping results into a repository.
  1. Update the repository as needed with the given timelapse.

# Details #

## Implementation ##

To perform these tasks, the pinger consists of these parts:

  * Repository for IP ranges to be pinged: **IIPRangesRepository**
  * Repository of lan machines, used for storing the ping results: **ILanHostsRepository**
  * Managing class that starts and creates pinger tasks to the task scheduler: **IPinger**
  * Task scheduler and/or thread pool that execute tasks: **ITaskExecutor**
  * Class that performs the concrete ping: **PingTask**

```
interface IIPRangesRepository : IList
{
    Save();
    Add(IPRange range);
    Add(IPRanges ranges);
    this[] {get; set; }
    Remove(int index);
}
```