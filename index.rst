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
* as a set, serve a broad range of science interests, but also
    * individually, significantly down-select the number of alerts per visit, and
    * individually, each meet a well-defined science goal,
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

