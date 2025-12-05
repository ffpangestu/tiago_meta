# Useful --ros-args commands
## 1. Remap names
Rename topics, services, or namespaces:
``` bash
--ros-args -r old_name:=new_name
--ros-args -r __ns:=/robot1
--ros-args -r __node:=camera_front
```

## 2. Set parameters
Provide parameters at startup:
``` bash
--ros-args -p speed:=1.5
--ros-args -p use_sim_time:=true
```

Load from a YAML file:
```bash
--ros-args --params-file config.yaml
```

## 3. Set DDS/domain

Change DDS domain (multi-robot isolation):
```bash
--ros-args -r __domain_id:=5
```

## 4. Control logging

Adjust verbosity:
```bash
--ros-args --log-level debug
--ros-args --log-level WARN
--ros-args --log-level my_pkg:=debug
```

## Example (multi-robot)
``` bash
ros2 run my_pkg lidar_node \
  --ros-args \
  -r __ns:=/robot2 \
  -r scan:=front_scan \
  --log-level INFO \
  -p max_range:=25.0 \
  --params-file robot2_lidar.yaml
```