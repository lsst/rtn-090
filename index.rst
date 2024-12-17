###########################################################
Roadmap for Community Alert Filters with the ANTARES Broker
###########################################################

.. abstract::

   This document guides the Rubin Community Science team’s work on Community Alert Filters for the ANTARES broker. The motivation, scope, and technical considerations for the community filters are described, and the timeline for community input and filter development is defined.


Overview
========

Requirements on the Rubin system specify that users will have access to alerts via predefined filters (Appendix A), hereafter referred to as "community filters."
These community filters are intended to provide a low barrier-to-entry starting point for community members wanting to start with alert science, and as such should cover a range of Rubin alert use cases.
The Rubin Community Science team (CST) will take input from the community to define, implement, and maintain the community filters.
The existence of community filters served by the CST does not preclude users from developing their own customized filters.
The (`ANTARES alert broker < https://nsf-noirlab.gitlab.io/csdc/antares/antares/ >`_) (`Matheson et al. (2021) < https://iopscience.iop.org/article/10.3847/1538-3881/abd703 >`_) provides functionality for user-defined filters.  Rubin is partnering with the ANTARES broker to host its community filters so as to meet requirements without constructing a bespoke Alert Filtering Service (`DMTN-226 <https://dmtn-226.lsst.io/>`_).

Scope
-----

The Rubin CST will:

#. Incorporate the Rubin science community’s input to develop, implement, test, and validate up to 20 Community Alert Filters in the ANTARES broker, starting with an initial set of ~5 filters during commissioning.
#. Provide documentation and use-case examples for the community filters.
#. Maintain and add to the set of community filters during Rubin Operations.

These community filters will:

* be designed to prevent redundancy among user-defined filters,
* together as a set, serve a broad range of science interests,
* individually, each meet a well-defined science goal,
* significantly down-select the number of alerts per visit,
* be subject to technical constraints, and
* be maintained throughout Rubin operations.

In order to serve a broad range of science interests, these filters should be simple to understand and prioritize completeness over purity.
For example, they would serve to down-select alerts for further real-time investigation by users (e.g., follow-up observations); they would not serve to define pure samples of unique astrophysical objects for population analysis.

Timeline
--------

This timeline guides the work of the Rubin Community Science team.

FY25 Q1, Oct-Dec 2024:

* prepare and release this tech note
* learn by implementing a few simple filters in ANTARES with ZTF

FY25 Q2, Jan-Mar 2025:

* prepare and advertise call input from the community
* review the input and draft ~5 initial community filters

FY25 Q3, Apr-Jun 2025 (or when LSST alerts begin):

* implement ~5 initial community filters
* release documentation and use-case tutorials

FY25 Q4, Jul-Sep 2025:

* prepare validation report and ‘lessons learned’ for the community

FY26 Q1, Oct-Dec 2026:

* second round of community input for additional community filters


Technical constraints
=====================

The following can be considered as rough guidelines.

Alert contents
--------------

See Section 3.5 of the Rubin Data Products Definitions Document (`LSE-163 <https://lse-163.lsst.io/>`_) for a list of alert packet contents, and `sdm-schemas.lsst.io/apdb.html <https://sdm-schemas.lsst.io/apdb.html>`_ has the as-implemented column names.

The community filters will use only the contents of the LSST alert packet plus any additional or derived data added by ANTARES, such as cross-matches with external (non-Rubin) catalogs performed by ANTARES.

The contents of the alert packets might evolve over Rubin Operations, thereby enabling new community filters.
For example, the final set of time series features to be computed during Alert Production remains to be determined (`DMTN-118 <https://dmtn-118.lsst.io/>`_).

Once a Rubin data release exists (DP2, DR1), the community filters will be able to query and use proprietary LSST data, such as multi-year light curves or the photo-z of potential host galaxies.

Processing limits
-----------------

The computational resources will be shared across all community filters, and thus what is available for a given filter will depend on the number of filters, their throughput, and the actual number of alerts per visit.

The LSST observing strategy will make one visit every ~30 seconds.
Any filter which takes, on average during the night, longer than 30 seconds per visit (~10,000 alerts) to process alerts from one visit will fall behind.

* Maximum latency per visit: 30 seconds (average over the night)

Follow-up feasibility
---------------------

The LSST Alerts: Key Numbers document (`DMTN-102 <https://dmtn-102.lsst.io/>`_) document predicts an average of 10,000 alert-triggering astrophysical sources per visit, with a maximum of >30,000 in Galactic fields.
The community filters should significantly sub-select the number of alerts per visit.
Filters that pass too many alerts do not sufficiently inform follow-up prioritization, which is the point of the filter.

* Average number of passing alerts per visit: 20 alerts
* Maximum number of passing alerts per visit: 100 alerts

Machine-learned models
----------------------

Community filters can be based on a trained ML model.

However, any community filters based on machine learning models would need to be trained and validated by volunteer members of the science community, training is beyond the scope of the Rubin CST.

Maintenance
-----------

The Rubin CST will maintain the community filters as ANTARES and LSST alerts evolve, in consultation with the user community.

Ideally, once a filter has been implemented it should be kept unchanged thereafter because users will build their analysis and follow-up programs on these community filters.
However, there may be cases where the filter is improved with community input (e.g., volunteer members of the science community re-train ML models), or where changes to the alert packet contents or ANTARES software necessitate an update to the filter.
Cases where the filter is unavoidably changed or deprecated will be advertised and documented for users.

To start, during commissioning the initial set of community filters will be limited to ~5 to allow room to grow without deactivating community filters unless necessary.


Calls for community input
=========================

The initial call for input to the community filters will invite everyone, as individuals or as teams, to contribute a short statement that either proposes a filter (in words or in code) or describes a science case that a filter should meet.

All contributions will be open and publicly viewable, so that others may see, upvote, and comment on them.
For this purpose, the Rubin Community Forum will be used in a similar way as it was used for the photometric redshift letters of recommendation process (`DMTN-049 <https://dmtn-049.lsst.io/>`_). 

The Rubin Community Science team (CST) will review and consolidate the input into the first ~5 community filters.
The CST will publicly post a summary of the input and descriptions of the community filters.
The community, the Science Advisory Committee, and the Users Committee will be invited to comment and refine the first ~5 filters before the CST implements them.

It is anticipated that a second call for input to the community filters would be repeated after one year, to define the next 5-10 community filters (and solicit improvements to the existing filters).
The timescale for future calls remains to be determined.


Appendix A
==========

Relevant references to community filters in Rubin requirements documentation.

LSST Science Requirements Document (`LPM-17 <https://docushare.lsst.org/docushare/dsweb/Get/LPM-17>`_)

* "The users will have an option of a query-like pre-filtering of this data stream in order to select likely candidates for specific transient type ... Several pre-defined filters optimized for traditionally popular transients, such as supernovae and microlensed sources, will also be available, as well as the ability to add new pre-defined filters as the survey continues." (Section 3.5)

LSST System Requirements document (`LSE-29 <https://docushare.lsst.org/docushare/dsweb/Get/LSE-29>`_)

* "Pre-defined filters optimized for traditionally popular transients shall be made available. It shall be possible for the project to add new pre-defined filters as the survey progresses ... The list of pre-defined filters, by way of example, should include ones for supernovae and microlensed sources." (LSR-REQ-0026)

Data Management System (DMS) Requirements document (`LSE-61 <https://docushare.lsst.org/docushare/dsweb/Get/LSE-61>`_)

* "A basic, limited capacity, alert filtering service shall be provided that can be given user defined filters to reduce the alert stream to manageable levels." (DMS-REQ-0342)

* "Users of the LSST Alert Filtering Service shall be able to use a predefined set of simple filters." (DMS-REQ-0348)

* "The LSST alert filtering service shall support numBrokerUsers (20) simultaneous users with each user allocated a bandwidth capable of receiving the equivalent of ``numBrokerAlerts`` (100) alerts per visit ... The constraint on number of alerts is specified for the full VOEvent alert content, but could also be satisfied by all alerts being received with minimal alert content." (DMS-REQ-0343)

Although not a requirements document, Section 3.5.2 of Version 3.9 of the Data Products Definitions Document (`LSE-163 <https://lse-163.lsst.io/>`_) details how users would receive and filter alerts.
The concept of community filters, as described in this tech note, is not represented in the DPDD and this document supersedes the DPDD on this topic.
