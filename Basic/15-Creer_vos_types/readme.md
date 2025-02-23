# **Creer vos propre type en solidity**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

// Code copied from optimism
// https://github.com/ethereum-optimism/optimism/blob/develop/packages/contracts-bedrock/src/dispute/lib/LibUDT.sol

type Duration is uint64;

type Timestamp is uint64;

type Clock is uint128;

library LibClock {
    function wrap(Duration _duration, Timestamp _timestamp)
        internal
        pure
        returns (Clock clock_)
    {
        assembly {
            // data | Duration | Timestamp
            // bit  | 0 ... 63 | 64 ... 127
            clock_ := or(shl(0x40, _duration), _timestamp)
        }
    }

    function duration(Clock _clock)
        internal
        pure
        returns (Duration duration_)
    {
        assembly {
            duration_ := shr(0x40, _clock)
        }
    }

    function timestamp(Clock _clock)
        internal
        pure
        returns (Timestamp timestamp_)
    {
        assembly {
            timestamp_ := shr(0xC0, shl(0xC0, _clock))
        }
    }
}

// Clock library without user defined value type
library LibClockBasic {
    function wrap(uint64 _duration, uint64 _timestamp)
        internal
        pure
        returns (uint128 clock)
    {
        assembly {
            clock := or(shl(0x40, _duration), _timestamp)
        }
    }
}

contract Examples {
    function example_no_uvdt() external view {
        // Without UDVT
        uint128 clock;
        uint64 d = 1;
        uint64 t = uint64(block.timestamp);
        clock = LibClockBasic.wrap(d, t);
        // Oops! wrong order of inputs but still compiles
        clock = LibClockBasic.wrap(t, d);
    }

    function example_uvdt() external view {
        // Turn value type into user defined value type
        Duration d = Duration.wrap(1);
        Timestamp t = Timestamp.wrap(uint64(block.timestamp));
        // Turn user defined value type back into primitive value type
        uint64 d_u64 = Duration.unwrap(d);
        uint64 t_u64 = Timestamp.unwrap(t);

        // LibClock example
        Clock clock = Clock.wrap(0);
        clock = LibClock.wrap(d, t);
        // Oops! wrong order of inputs
        // This will not compile
        // clock = LibClock.wrap(t, d);
    }
}
```

## Execute sur Remix
[créer_vos_type.sol](https://remix.ethereum.org/?#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC4yNjsKCi8vIENvZGUgY29waWVkIGZyb20gb3B0aW1pc20KLy8gaHR0cHM6Ly9naXRodWIuY29tL2V0aGVyZXVtLW9wdGltaXNtL29wdGltaXNtL2Jsb2IvZGV2ZWxvcC9wYWNrYWdlcy9jb250cmFjdHMtYmVkcm9jay9zcmMvZGlzcHV0ZS9saWIvTGliVURULnNvbAoKdHlwZSBEdXJhdGlvbiBpcyB1aW50NjQ7Cgp0eXBlIFRpbWVzdGFtcCBpcyB1aW50NjQ7Cgp0eXBlIENsb2NrIGlzIHVpbnQxMjg7CgpsaWJyYXJ5IExpYkNsb2NrIHsKICAgIGZ1bmN0aW9uIHdyYXAoRHVyYXRpb24gX2R1cmF0aW9uLCBUaW1lc3RhbXAgX3RpbWVzdGFtcCkKICAgICAgICBpbnRlcm5hbAogICAgICAgIHB1cmUKICAgICAgICByZXR1cm5zIChDbG9jayBjbG9ja18pCiAgICB7CiAgICAgICAgYXNzZW1ibHkgewogICAgICAgICAgICAvLyBkYXRhIHwgRHVyYXRpb24gfCBUaW1lc3RhbXAKICAgICAgICAgICAgLy8gYml0ICB8IDAgLi4uIDYzIHwgNjQgLi4uIDEyNwogICAgICAgICAgICBjbG9ja18gOj0gb3Ioc2hsKDB4NDAsIF9kdXJhdGlvbiksIF90aW1lc3RhbXApCiAgICAgICAgfQogICAgfQoKICAgIGZ1bmN0aW9uIGR1cmF0aW9uKENsb2NrIF9jbG9jaykKICAgICAgICBpbnRlcm5hbAogICAgICAgIHB1cmUKICAgICAgICByZXR1cm5zIChEdXJhdGlvbiBkdXJhdGlvbl8pCiAgICB7CiAgICAgICAgYXNzZW1ibHkgewogICAgICAgICAgICBkdXJhdGlvbl8gOj0gc2hyKDB4NDAsIF9jbG9jaykKICAgICAgICB9CiAgICB9CgogICAgZnVuY3Rpb24gdGltZXN0YW1wKENsb2NrIF9jbG9jaykKICAgICAgICBpbnRlcm5hbAogICAgICAgIHB1cmUKICAgICAgICByZXR1cm5zIChUaW1lc3RhbXAgdGltZXN0YW1wXykKICAgIHsKICAgICAgICBhc3NlbWJseSB7CiAgICAgICAgICAgIHRpbWVzdGFtcF8gOj0gc2hyKDB4QzAsIHNobCgweEMwLCBfY2xvY2spKQogICAgICAgIH0KICAgIH0KfQoKLy8gQ2xvY2sgbGlicmFyeSB3aXRob3V0IHVzZXIgZGVmaW5lZCB2YWx1ZSB0eXBlCmxpYnJhcnkgTGliQ2xvY2tCYXNpYyB7CiAgICBmdW5jdGlvbiB3cmFwKHVpbnQ2NCBfZHVyYXRpb24sIHVpbnQ2NCBfdGltZXN0YW1wKQogICAgICAgIGludGVybmFsCiAgICAgICAgcHVyZQogICAgICAgIHJldHVybnMgKHVpbnQxMjggY2xvY2spCiAgICB7CiAgICAgICAgYXNzZW1ibHkgewogICAgICAgICAgICBjbG9jayA6PSBvcihzaGwoMHg0MCwgX2R1cmF0aW9uKSwgX3RpbWVzdGFtcCkKICAgICAgICB9CiAgICB9Cn0KCmNvbnRyYWN0IEV4YW1wbGVzIHsKICAgIGZ1bmN0aW9uIGV4YW1wbGVfbm9fdXZkdCgpIGV4dGVybmFsIHZpZXcgewogICAgICAgIC8vIFdpdGhvdXQgVURWVAogICAgICAgIHVpbnQxMjggY2xvY2s7CiAgICAgICAgdWludDY0IGQgPSAxOwogICAgICAgIHVpbnQ2NCB0ID0gdWludDY0KGJsb2NrLnRpbWVzdGFtcCk7CiAgICAgICAgY2xvY2sgPSBMaWJDbG9ja0Jhc2ljLndyYXAoZCwgdCk7CiAgICAgICAgLy8gT29wcyEgd3Jvbmcgb3JkZXIgb2YgaW5wdXRzIGJ1dCBzdGlsbCBjb21waWxlcwogICAgICAgIGNsb2NrID0gTGliQ2xvY2tCYXNpYy53cmFwKHQsIGQpOwogICAgfQoKICAgIGZ1bmN0aW9uIGV4YW1wbGVfdXZkdCgpIGV4dGVybmFsIHZpZXcgewogICAgICAgIC8vIFR1cm4gdmFsdWUgdHlwZSBpbnRvIHVzZXIgZGVmaW5lZCB2YWx1ZSB0eXBlCiAgICAgICAgRHVyYXRpb24gZCA9IER1cmF0aW9uLndyYXAoMSk7CiAgICAgICAgVGltZXN0YW1wIHQgPSBUaW1lc3RhbXAud3JhcCh1aW50NjQoYmxvY2sudGltZXN0YW1wKSk7CiAgICAgICAgLy8gVHVybiB1c2VyIGRlZmluZWQgdmFsdWUgdHlwZSBiYWNrIGludG8gcHJpbWl0aXZlIHZhbHVlIHR5cGUKICAgICAgICB1aW50NjQgZF91NjQgPSBEdXJhdGlvbi51bndyYXAoZCk7CiAgICAgICAgdWludDY0IHRfdTY0ID0gVGltZXN0YW1wLnVud3JhcCh0KTsKCiAgICAgICAgLy8gTGliQ2xvY2sgZXhhbXBsZQogICAgICAgIENsb2NrIGNsb2NrID0gQ2xvY2sud3JhcCgwKTsKICAgICAgICBjbG9jayA9IExpYkNsb2NrLndyYXAoZCwgdCk7CiAgICAgICAgLy8gT29wcyEgd3Jvbmcgb3JkZXIgb2YgaW5wdXRzCiAgICAgICAgLy8gVGhpcyB3aWxsIG5vdCBjb21waWxlCiAgICAgICAgLy8gY2xvY2sgPSBMaWJDbG9jay53cmFwKHQsIGQpOwogICAgfQp9Cg&lang=fr&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.26+commit.8a97fa7a.js)