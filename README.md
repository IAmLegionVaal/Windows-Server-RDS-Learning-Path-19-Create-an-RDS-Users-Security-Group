# Windows Server RDS Learning Path 19 — Create an RDS Users Security Group

**Level:** Intermediate · **Module:** 19/70

## Goal
Create and manage the domain security group that controls access to the RDS collection.

## Setup
1. Create `GG-RDS-Users` in `OU=Groups,OU=RDS` if it does not already exist.
2. Add only approved normal test users.
3. Document the group owner, purpose and review date.
4. Confirm privileged administrative identities are not members.
5. Refresh user tokens after membership changes.

```powershell
Get-ADGroup GG-RDS-Users -Properties Description,ManagedBy,Members
Get-ADGroupMember GG-RDS-Users
Add-ADGroupMember GG-RDS-Users rdsuser1,rdsuser2
Get-ADPrincipalGroupMembership rdsuser1 | Select-Object Name,GroupScope
```

## Evidence
Save group properties, membership before/after, owner/review notes and user token validation under `evidence/`. Record every membership change and final pass/fail state.

## Troubleshooting
Use exact samAccountName or distinguished name when adding members. Sign out and back in before concluding new membership is ineffective.

## Security
Collection access must use a dedicated group rather than individual ACL entries or broad groups such as Domain Users.

## Rollback
Remove only disposable test memberships; preserve the group for later modules.

## Next
`Windows-Server-RDS-Learning-Path-20-Assign-Users-to-the-RDS-Collection`
