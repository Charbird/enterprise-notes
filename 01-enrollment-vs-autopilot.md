# Windows Autopilot is not required for Intune enrollment

I have seen this question floating around a lot recently, so here is a quick emergency explainer.  
Autopilot is powerful, but it is not a requirement for getting devices into Intune.

---

## Who can enroll devices into Intune

Enrollment happens through permissions, not Autopilot.

- **Users with MDM enrollment rights**  
  - Set in Azure AD under Mobility (MDM and MAM).  
  - Controlled by group assignment such as All Users or a dedicated Intune Enrollers group.  
  - By default each user can enroll up to 5 devices, configurable in Azure AD.

- **Enrollment administrators**  
  - Accounts with rights to bulk enroll devices. Useful for IT-led setups.

- **Device Enrollment Manager (DEM)**  
  - Legacy option that allows one account to enroll many devices. Rarely needed today.

If users have corporate enrollment rights, they can bring devices into Intune without Autopilot.

---

## Device type restrictions

Device type restrictions define which devices are allowed to enroll:

- Platforms (Windows, iOS, Android, macOS)  
- Minimum or maximum OS versions  
- Personally owned devices (allow or block)

This is where you control what is allowed into your environment at the point of enrollment.

---

## Converting enrolled devices to Autopilot

Deployment profiles include a setting: **Convert all targeted devices to Autopilot**.

- When set to Yes, any device that enrolls will have its hardware hash uploaded automatically.  
- This lets you build your Autopilot device list over time without manual hash collection.  
- The device is already managed by Intune, and the Autopilot step comes later.

---

## Where Autopilot adds value

Autopilot is most useful for:  
- Streamlined out of box experience (naming, Entra join, userless kiosk)  
- Direct provisioning from vendor to user  
- Reset and redeploy scenarios  

It is not required for:  
- First time Intune enrollment  
- Ongoing device management  

---

## Closing thought

Autopilot is an accelerator, not a gatekeeper.  
Start with enrollment permissions and restrictions, then add Autopilot when you want the extra polish or lifecycle benefits.
