Starting a New Scenario
============================

Problem Definition
--------------------

We will start with a new scenario representing a simplified once-through fuel
cycle.  For the purpose of this tutorial, the scenario will include:

* mine of natural uranium
* enrichment facility producing 4% enriched uranium oxide fuel
* LWR reactor consuming fresh fuel and producing used fuel
* repository to house all spent fuel

More details about each of these facilities will discussed when we are
required to provide that input.

Concept: Simulation Time Steps
------------------------------

CYCLUS uses a time-step approach to march through time and determine what
actions are taken by each agent at each point in time.  Each time step
includes the following phases:

* new agents may enter the system (deployment)
* each agent prepares for exchange of material
* agents engage in material trades
* each agent acts after the exchange of material
* agents may leave the system (decommissioning)

Users do not have to manage these phases, but must provide the following
information for all simulations:

1. <simulation>:  The simulation handle contains all the parameters in the simulation.

2. <duration>: the number of months to be simulated

3. <startmonth>: the first month of the simulation (e.g.: 1 for January)

4. <startyear>: the first year of the simulation

5. <decay>:The Cyclus kernel has built-in experimental support for `Decay <http://fuelcycle.org/devdoc/decay.html>`_ calculations. Materials store the time since their last decay and agents are free to invoke the decay function on them as desired to decay them to the current simulation time. Cyclus can operate in 3 decay modes, with 1 additional mode likely to be added in a future release:

- 'never' if all decay is turned off
- 'manual', meaning it is only on if the individual archetype decays their own inventory
- 'lazy', which will compute decay only when archetypes fetch a particular composition.
- 'periodic' (future) automatically decays all materials in a simulation with some fixed frequency. 

There are other `optional parameters <http://fuelcycle.org/user/input_specs/control.html>`_ that
could be given but are not in the scope of this tutorial.


6. Description: A brief description of your simulation.

We'll return later to the topics of generating, loading and executing an input file.


The simulation control is the first part of the CYCLUS input file and is of the form:

::

    <simulation>
      <control>
        <duration>duration_val</duration>
        <startmonth>start_month_val</startmonth>
        <startyear>start_year_val</startyear>
        <decay>decay_val</decay>
      </control>


    </simulation>

The lifetime of a *CYCLUS* simulation is determined by its
**duration**. **duration** is the number of months *CYCLUS* will
model the fuel cycle. *CYCLUS* also intakes the **start_month** and
**start_year** of the simulation. The last major parameter of the
simulation is whether or not we wish to model the
`decay <http://fuelcycle.org/devdoc/decay.html>`__ of the
radioactive elements (uranium ore, nuclear fuel, & spent nuclear fuel)
in the simulation. For simplicity, we will not model decay in this
tutorial.

Activity: Set Simulation Parameters
-----------------------------------
Using the simulation control template above and the table below, properly fill the template with the variables listed in the table below in your favorite text editor

+-------------------+---------------+---------------------------------+
| Variable          | Value         | Purpose                         |
+===================+===============+=================================+
| ``duration``      | ``720``       | length of simulation (months)   |
+-------------------+---------------+---------------------------------+
| ``start_month``   | ``1``         | start month of simulation       |
+-------------------+---------------+---------------------------------+
| ``start_year``    | ``2018``      | start year of simulation        |
+-------------------+---------------+---------------------------------+
| ``decay``         | ``never``     | radioactive decay               |
+-------------------+---------------+---------------------------------+

Using this table, let's set the simulation parameters.

1. To tell CYCLUS that this is the simulation section of the input file, set  the first line of the input file to be:
::

    <simulation>

2. Place the ``control`` header in as such

::

  <simulation>
    <control>

If you would like, you can space or tab the ``control`` header over for personal ease of reading the file but it is not necessary.

3. After filling in the parameters listed in the table above tab out and close the control and simulation sections as:

::

    <simulation>
      <control>
        <duration>720</duration>
        <startmonth>1</startmonth>
        <startyear>2018</startyear>
        <decay>never</decay>
      </control>


    </simulation>

**Note**: There is two spaces between the end of the control section and end of the simulation section as the simulation section will hold the commodities, facilities, regions, institutions, and recipe information.
