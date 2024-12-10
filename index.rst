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
The existence of community filters served by the CST do not preclude users from developing their own customized filters.
The ANTARES alert broker provides the functionality for user-defined filters, and the ANTARES team has agreed to host these community filters, so that Rubin Operations can meet these requirements without constructing an Alert Filtering Service (`DMTN-226 <https://dmtn-226.lsst.io/>`_).

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
