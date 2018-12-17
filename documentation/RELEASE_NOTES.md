# pvaClientCPP Module

This document summarizes the changes to the module between releases.


## Release 4.4 (EPICS 7.0.2, Dec 2018)

### API changes to PvaClientMonitor

The create method that had arguments for stateChangeRequester and monitorRequester no longer exists.

### API changes to PvaClientGet, ..., PvaClientMonitor

Previously the pvaClientGet, ..., pvaClientMonitor classes all implemented PvaClientChannelStateChangeRequester(). This method was never called and has been removed.


## Release 4.3 (EPICS 7.0.1, Dec 2017)

### Requires pvDataCPP-7.0 and pvAccessCPP-6.0 versions

This release will not work with older versions of these modules.

### Destroy methods removed

All the destroy() methods have been removed, implementation is RAII compliant.

### API changes to PvaClientMonitor

The second argument of method

    static PvaClientMonitorPtr create(
        PvaClientPtr const &pvaClient,
        epics::pvAccess::Channel::shared_pointer const & channel,
        epics::pvData::PVStructurePtr const &pvRequest
    );

is now changed to

    static PvaClientMonitorPtr create(
        PvaClientPtr const &pvaClient,
        PvaClientChannelPtr const & pvaClientChannel,
        epics::pvData::PVStructurePtr const &pvRequest
    );

A new method is also implemented

    static PvaClientMonitorPtr create(
        PvaClientPtr const &pvaClient,
        std::string const & channelName,
        std::string const & providerName,
        std::string const & request,
        PvaClientChannelStateChangeRequesterPtr const & stateChangeRequester,
        PvaClientMonitorRequesterPtr const & monitorRequester
    );


## Release 4.2 (EPICS V4.6, Aug 2016)

* The examples are moved to exampleCPP.
* Support for channelRPC is now available.
* In PvaClientMultiChannel checkConnected() now throws an exception if connect fails.


## Release 4.1 (EPICS V4.5, Oct 2015)

pvaClient is a synchronous API for pvAccess.

This is the first release of pvaClientCPP.
It provides an API that is similar to pvaClientJava.
