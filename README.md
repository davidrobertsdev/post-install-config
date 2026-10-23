
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Post-Install Configuration</h1>
This tutorial walks through the post-installation configuration of the open-source help desk ticketing system osTicket (v1.15.8). After a fresh install, osTicket only contains generic default settings. Here we tailor it to a realistic support environment by adding custom help topics, severity-based SLA plans, a support team, and a custom agent role, then verify everything by submitting a test ticket as an end user.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- osTicket v1.15.8
- Microsoft Edge (Admin Panel and end-user portal)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Prerequisites</h2>

- A working osTicket installation (see the <b>osTicket - Prerequisites and Installation</b> tutorial)
- Access to the osTicket <b>Admin Panel</b> at <code>http://localhost/osTicket/scp</code> using the admin account created during installation
- Access to the end-user portal at <code>http://localhost/osTicket/</code> to test the configuration

<h2>Post-Install Configuration Objectives</h2>

- Create custom <b>Help Topics</b> so end users can categorize their issues
- Create <b>SLA plans</b> that set response expectations by severity (Sev-A, Sev-B, Sev-C)
- Create a <b>Team</b> to group agents who handle a specific type of ticket
- Create a custom <b>Role</b> to control what agents are allowed to do
- Submit a <b>test ticket</b> as an end user to confirm the configuration works

<h2>Configuration Steps</h2>

<h3>Part 1: Help Topics</h3>

<p>
<img src="https://github.com/user-attachments/assets/2054f019-893b-4a22-99c6-55e4462c2caa" height="80%" width="80%" alt="Default help topics"/>
</p>
<p>
<b>Step 1: Review the default Help Topics.</b>
<br />1. Log in to the Admin Panel.
<br />2. Click the <b>Manage</b> tab, then select <b>Help Topics</b>.
<br /><br />
Help Topics are the categories an end user picks from when opening a ticket, and each one can automatically route the ticket to a department, set its priority, and apply an SLA. A fresh install includes four defaults: <b>Feedback</b> (Low priority), <b>General Inquiry</b>, <b>Report a Problem</b>, and <b>Report a Problem / Access Issue</b> (High priority). All four are Active, Public, and assigned to the Support department.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/aa057c81-dc08-4d10-a0b5-c638e6cc46ed" height="80%" width="80%" alt="Help topics with new entries added"/>
</p>
<p>
<b>Step 2: Add custom Help Topics.</b>
<br />1. Click <b>Add New Help Topic</b>.
<br />2. Enter a <b>Topic</b> name, set the <b>Status</b> to Active, and the <b>Type</b> to Public so it shows up for end users.
<br />3. Choose the <b>Department</b> (Support) and a <b>Priority</b>.
<br />4. Click <b>Save Changes</b>, then repeat for each topic.
<br /><br />
I created <b>Business Critical Outage</b> and <b>Personal Equipment failure</b>. After saving, the list shows both new entries alongside the defaults, each with its created and last-updated timestamps. Topics that reflect real scenarios make it much easier to triage tickets later.
</p>
<br />

<h3>Part 2: Service Level Agreements (SLAs)</h3>

<p>
<img src="https://github.com/user-attachments/assets/649206f3-f731-41bd-a0b5-7b85ffdccfb5" height="80%" width="80%" alt="Default SLA plan"/>
</p>
<p>
<b>Step 3: Review the default SLA.</b>
<br />1. Click <b>Manage</b>, then <b>SLA</b>.
<br /><br />
Only the <b>Default SLA</b> exists at first, with an <b>18-hour grace period</b>. The grace period is how long an agent has to respond before a ticket is marked overdue. One 18-hour window for every ticket is too loose for a real help desk, since an outage and a general question should not wait the same amount of time.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/17d555b6-69a7-41b9-be55-de955b10aeab" height="80%" width="80%" alt="Custom SLA plans"/>
</p>
<p>
<b>Step 4: Create severity-based SLA plans.</b>
<br />1. Click <b>Add New SLA Plan</b>.
<br />2. Enter a name and set the <b>Grace Period</b> in hours.
<br />3. Make sure the status is Active and save.
<br />4. Repeat for each tier.
<br /><br />
I created three plans:
<br />- <b>Sev-A:</b> 1-hour grace period (most urgent, such as outages)
<br />- <b>Sev-B:</b> 4-hour grace period
<br />- <b>Sev-C:</b> 8-hour grace period (least urgent)
<br /><br />
These SLAs can then be attached to help topics, so a Business Critical Outage ticket is held to a much tighter deadline than general feedback.
</p>
<br />

<h3>Part 3: Teams and Roles</h3>

<p>
<img src="https://github.com/user-attachments/assets/6eaf66f9-bbd2-49fc-98b3-c169f141ebbb" height="80%" width="80%" alt="Creating the Online Banking team"/>
</p>
<p>
<b>Step 5: Create a Team.</b>
<br />1. Click the <b>Agents</b> tab, then select <b>Teams</b>.
<br />2. Click <b>Add New Team</b>.
<br />3. Enter the team name, set the <b>Status</b> to Active, and optionally choose a <b>Team Lead</b>.
<br />4. Click <b>Save Changes</b>.
<br /><br />
I created a team named <b>Online Banking</b> with no team lead assigned. Teams let tickets be assigned to a group of agents instead of one person, and agents can be added from the <b>Members</b> tab. The <b>Assignment Alert</b> checkbox controls whether the team is notified when a ticket is assigned to it, and I left it enabled.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/acc72737-dd20-4799-9b9f-3feefe09a1d3" height="80%" width="80%" alt="Adding a new role"/>
</p>
<p>
<b>Step 6: Create a custom Role.</b>
<br />1. Click <b>Agents</b>, then <b>Roles</b>.
<br />2. Click <b>Add New Role</b>.
<br />3. On the <b>Definition</b> tab, enter the role name. I used <b>Supreme Admin</b>.
<br />4. Open the <b>Permissions</b> tab and select the permissions this role should have (ticket creation, editing, assignment, closing, deleting, and so on).
<br />5. Click <b>Add Role</b>.
<br /><br />
Roles define what an agent is allowed to do inside the help desk. Creating a dedicated role is better than editing the defaults, because the built-in roles stay available as a baseline.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/5e2c0dfd-62bc-4a93-af70-58ee4409d7c1" height="80%" width="80%" alt="Roles list showing Supreme Admin"/>
</p>
<p>
<b>Step 7: Confirm the new Role.</b>
<br />The Roles list now shows <b>Supreme Admin</b> (circled) alongside the built-in roles: <b>All Access</b>, <b>Expanded Access</b>, <b>Limited Access</b>, and <b>View only</b>. The Supreme Admin role is Active and shows the time it was created. It can now be assigned to agents when they are added to a department.
</p>
<br />


<h2>Summary</h2>

By the end of this lab, osTicket is configured with custom help topics, tiered SLA plans, a team, and a custom role. These are the same building blocks a real IT help desk uses to route, prioritize, and track support requests.
