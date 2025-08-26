# AD/SCCM ≠ Entra ID/Intune — Understanding the Real Difference

This post came out of an unique network migration project I’ve been working on.  
It reminded me how easy it is to assume **Active Directory (AD) + SCCM** are a direct precursor to **Entra ID + Intune**.  

On the surface they look like replacements:  
- AD ↔ Entra ID (directory of people and devices)  
- SCCM ↔ Intune (managing devices, patching, deploying apps)  

But that’s misleading. They’re not the same thing at all.  
It’s like comparing a **bird** and a **bat**. Both can fly, but they’re built on very different biology.  

---

## AD/SCCM — Boundary-Based Trust

- AD was designed for a **trusted network perimeter**.  
- Devices are joined to the domain → they inherit trust.  
- Authentication: NTLM/Kerberos inside the “castle.”  
- SCCM assumes devices are always reachable inside that boundary.  
- Common practice: generic accounts like `student1` work fine, because trust flows from the network and domain object.  
- File shares are accessible because both the device and user account live inside the boundary.  

---

## Entra ID/Intune — Identity-First Trust

- Entra ID assumes **zero trust, cloud-first**.  
- Devices don’t trust each other just because they’re “joined.”  
- Authentication: modern protocols (OAuth, OpenID Connect), token-based.  
- Intune evaluates device telemetry and compliance per session.  
- Access is granted only after **identity + device state + Conditional Access** say “yes.”  
- Licensing and compliance attach to the *person* and the *device*, not the network.  
- Generic logins break down, because the whole platform is built on **identity-first licensing and trust**.  

---

## A Simple Example

- **In AD**: A lab machine joined to the domain can access a local file share. Generic account `student1` logs on → share access works because the machine and user are trusted in the domain.  

- **In Entra/Intune**: That same lab machine can’t just talk to another. No inherent trust, no Kerberos. Instead:  
  - The user must sign in with a licensed identity.  
  - The device must meet compliance.  
  - Conditional Access decides if the session gets OneDrive/SharePoint/Azure Files.  

Same outcome (student saves a file), but *completely different logic*.  

---

## Why It Matters

If you design for Entra/Intune as if it were “AD in the cloud,” you’ll quickly get stuck.  

Boundary-based thinking doesn’t translate to an identity-first model.  
To succeed, you need to shift mental models:  

- **AD/SCCM = Boundary-first**  
- **Entra/Intune = Identity-first**  

That shift is the foundation for modern cloud design.  

---
