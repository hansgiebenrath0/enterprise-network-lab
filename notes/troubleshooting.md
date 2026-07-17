# Troubleshooting Notes

This document records issues encountered during the implementation of the Enterprise Network Lab and their solutions.

---

# Packet Tracer Limitations

## Running Configuration

### Issue

The following command is not supported in Packet Tracer:

```cisco
show running-config interface FastEthernet0/1
```

### Solution

Use:

```cisco
show running-config | section FastEthernet0/1
```

---

# Empty MAC Address Table

### Issue

Initially, the MAC address table appeared empty.

### Cause

Packet Tracer only learns MAC addresses after traffic is generated.

### Solution

Generate traffic using:

```text
ping
```

and verify again using:

```cisco
show mac address-table
```

---

# Port Security Recovery

### Issue

After recovering from a Port Security violation, the interface remained blocked.

### Cause

Packet Tracer kept the previously learned Sticky MAC address associated with the interface.

### Solution

Remove the learned Sticky MAC explicitly.

Example:

```cisco
interface FastEthernet0/1

no switchport port-security mac-address sticky 00D0.97E9.2A1A

shutdown

no shutdown
```

The interface then accepted a new Sticky MAC after traffic was generated.

---

# Packet Tracer Behavior

Some Packet Tracer versions may retain dynamic security entries longer than expected.

Always verify:

```cisco
show port-security address

show port-security interface
```

before assuming the configuration is incorrect.

---

# BPDU Guard Disabled an Access Port

## Problem

After connecting another switch to an access port, network connectivity was immediately lost.

The interface entered the **err-disabled** state.

Verification command:

```text
show interface fa0/2
```

Example output:

```text
FastEthernet0/2 is down, line protocol is down (err-disabled)
```

---

## Cause

The access port was configured with:

- PortFast
- BPDU Guard

When a second switch was connected, it transmitted Bridge Protocol Data Units (BPDUs).

BPDU Guard detected the BPDU and immediately disabled the interface to prevent a potential Layer 2 loop.

This is the expected behavior on Cisco switches.

---

## Solution

Disconnect the unauthorized switch.

Recover the interface by resetting it.

```cisco
conf t
interface fa0/2
shutdown
no shutdown
end
```

Verify the interface status:

```text
show interface fa0/2
```

The interface should return to the **up/up** state.

---

## Lessons Learned

BPDU Guard should be enabled on all PortFast access ports.

If an unauthorized switch is connected, the affected interface is automatically disabled, protecting the network from switching loops.

Always verify that only end devices are connected to PortFast-enabled interfaces.