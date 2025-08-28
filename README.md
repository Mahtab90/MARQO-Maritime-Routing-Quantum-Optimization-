TRAMP_TSP_BIG_v1 (TSP/VRP-STYLE)

Zip: TRAMP_TSP_BIG_v1.zip
Contents:

tsp_ports.csv (300 ports; coordinates in nautical miles; base capacities)

tsp_vessels.csv (120 vessels)

tsp_routes.csv (10–25 visits per vessel; service times in hours)

tsp_distances.csv (complete 300×299 directed distance matrix; ~89,700 rows)

tsp_constraints.csv (base capacities plus 50 exclusivity rules)

README.txt (notes)

Dataset purpose:

Large synthetic benchmark for constrained routing (TSP/VRP-like) with port capacity and conditional exclusivity rules.

Suitable for CP-SAT, MILP, metaheuristics, and quantum/hybrid demos.

Fully synthetic; coordinates on a jittered grid; distances are Euclidean in nm; sailing time derived at 18 knots.

Schemas:

tsp_ports.csv
port_id: string (e.g., P001)
name: string
capacity_base: integer (max simultaneous vessels)
x_nm: float (x coordinate in nm)
y_nm: float (y coordinate in nm)

tsp_vessels.csv
vessel_id: string (e.g., V001)
name: string
start_node: string (use as depot if needed)

tsp_routes.csv
vessel_id: string
sequence_order: integer (visit order per vessel)
port_id: string
service_time_hours: float

tsp_distances.csv
from_port: string
to_port: string
distance_nm: float
sailing_hours_at_18kn: float

tsp_constraints.csv
type: string ("capacity" or "capacity_override_if_vessel_present")
port_id: string
vessel_id: string or empty (used only for overrides)
parameter: string ("max_vessels_simultaneous")
value: integer (capacity value)
units: string ("vessels")
note: string

Constraint semantics:

Capacity: at any time, concurrent vessels at a port must be less than or equal to capacity_base.

Exclusive access: while the specified vessel is present at a port, the port capacity is overridden to the given value (typically 1).

Typical objectives:

Minimize total completion time or makespan.

Minimize sailing time plus service time.

Minimize weighted delays subject to capacities and exclusivity.
----------------------------------------------------------------------
BAP_TW_BIG_v1 (BERTH ALLOCATION WITH TIME WINDOWS)

Zip: BAP_TW_BIG_v1.zip
Contents:

bap_terminals.csv (40 terminals; berth capacities 2–8)

bap_vessels.csv (2,000 vessels over a 7-day horizon; ETA windows and service times)

bap_constraints.csv (base capacities plus 100 exclusivity rules)

README.txt (notes)

Dataset purpose:

Large synthetic benchmark for berth allocation with time windows and conditional capacity rules.

Suitable for CP-SAT/MILP scheduling, constraint programming, and quantum/hybrid demos on congestion reduction.

Fully synthetic; ETA windows distributed over one week.

Schemas:

bap_terminals.csv
terminal_id: string (e.g., T01)
name: string
berth_capacity: integer (max simultaneous vessels)

bap_vessels.csv
vessel_id: string (e.g., S0001)
type: string (Container, RoRo, Bulk, Tanker, General, CarCarrier)
preferred_terminal: string
eta_earliest: ISO-8601 datetime
eta_latest: ISO-8601 datetime
service_time_hours: float

bap_constraints.csv
type: string ("capacity" or "capacity_override_if_vessel_present")
terminal_id: string
vessel_id: string or empty (used only for overrides)
parameter: string ("berth_capacity")
value: integer (capacity value)
units: string ("berths")
note: string

Constraint semantics:

Capacity: at any time, the number of berthed vessels at a terminal must be less than or equal to berth_capacity.

Exclusive access: while the specified vessel is present at a terminal, the terminal capacity is overridden to the given value (for example, 1 or 2).

Typical objectives:

Minimize total waiting or anchorage.

Minimize penalties for lateness beyond eta_latest.

Maximize on-time berthing subject to capacities and exclusivity.
