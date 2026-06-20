# OXY LIVE STABLE CHECKLIST

**Project:** DubleOxy / OXY / OXY AUT  
**File:** `docs/OXY_LIVE_STABLE_CHECKLIST.md`  
**Status:** Read-only checklist / planning document. No server changes. No code changes.  
**Purpose:** Verify the current OXY live state before moving to AlmaLinux / VM101 work.

---

## 1. Purpose

This document defines the read-only checklist for confirming that OXY live is stable enough to pause safely before AlmaLinux / VM101 work.

This checklist does not change the server.

```text
No code changes.
No live UI changes.
No nginx changes.
No VM changes.
No public access changes.
```

---

## 2. Current live OXY base

Confirmed current live base:

```text
VM 100 = biroro-main
IP: 192.168.1.252
Live URL: http://192.168.1.252
Web root: /var/www/oxy/current/public
Live file: /var/www/oxy/current/public/index.html
```

---

## 3. Read-only checks

### 3.1 Confirm live URL responds

Read-only check:

```bash
curl -I http://192.168.1.252
```

Expected:

```text
HTTP/1.1 200 OK
or another valid HTTP response proving nginx/site responds
```

Do not edit anything.

---

### 3.2 Confirm local web server responds from VM100

If already inside VM100:

```bash
curl -I http://127.0.0.1
```

Expected:

```text
HTTP/1.1 200 OK
```

Do not restart nginx unless a separate stage is approved.

---

### 3.3 Confirm nginx status read-only

```bash
systemctl status nginx --no-pager
```

Expected:

```text
active (running)
```

Do not run restart/reload unless approved.

---

### 3.4 Confirm SSH status read-only

```bash
systemctl status ssh --no-pager
```

Expected:

```text
active (running)
```

---

### 3.5 Confirm live directory

```bash
ls -la /var/www/oxy/current/public
```

Expected known files:

```text
index.html
index_BEFORE_REMOVE_CHTCHTO.html
index_LIVE_WITH_PROMO_AI_FOUND.html
i1-layout-preview.html
i1-standalone-preview.html
oxy_formula_search.txt
oxy_formula_search_CLEAN.txt
oxy_formula_search_EXACT.txt
oxy_formula_search_STRONG.txt
```

Do not delete, rename, or overwrite files.

---

### 3.6 Confirm live index exists

```bash
test -f /var/www/oxy/current/public/index.html && echo "index.html exists"
```

Expected:

```text
index.html exists
```

---

### 3.7 Confirm index size / timestamp read-only

```bash
stat /var/www/oxy/current/public/index.html
```

Purpose:

```text
record current size and modification time before future stages
```

Do not edit.

---

### 3.8 Confirm backups exist

```bash
ls -la /var/www/oxy/current/public/index_* /var/www/oxy/current/public/*BACKUP* 2>/dev/null
```

Expected at least:

```text
index_BEFORE_REMOVE_CHTCHTO.html
index_LIVE_WITH_PROMO_AI_FOUND.html
```

---

### 3.9 Confirm no public router/DNS stage is active

Manual/read-only status:

```text
No router port forwarding should be enabled for OXY.
No public DNS should point to LAN OXY.
No public IP exposure should be configured.
No DMZ should be enabled for VM100.
```

---

## 4. UI checks by browser

Open:

```text
http://192.168.1.252
```

Check visually:

```text
OXY page loads.
Main interface is visible.
No blank page.
No obvious broken layout.
No accidental debug text in visible UI.
No unexpected "чтчто" typo.
Access/trial/registration UI is not broken.
```

Do not edit through browser or devtools.

---

## 5. OXY modules separation check

Confirm these remain separate from live integration unless approved:

```text
OXY Generator
OXY Constructor
OXY AUT
Hidden Editor
OXYFootballCycle.js
tests/hidden_editor_preview.html
tests/oxy_football_cycle_test.js
```

Rule:

```text
No hidden editor live connection yet.
No generator direct live merge yet.
No constructor direct live merge yet.
```

---

## 6. GitHub docs checkpoint

Confirm these docs exist in GitHub:

```text
docs/OXY_CONTROL_POINT_BEFORE_ALMALINUX.md
docs/OXY_LIVE_STABLE_CHECKLIST.md
docs/SERVER_PROJECTS_MASTER_MAP.md
docs/PROXMOX_READONLY_INVENTORY.md
docs/VM101_CREATE_DRAFT.md
docs/VM101_PANEL_DECISION_MATRIX.md
docs/OXY_SERVER_CURRENT_INVENTORY.md
docs/OXY_DO_NOT_TOUCH.md
```

---

## 7. Do not touch list

Do not touch without separate approval:

```text
VM 100
nginx
/var/www/oxy/current/public/index.html
live UI
headers / шапки
i1 / i2 / i3
iframe/srcdoc
license / access / trial UI
src/oxy-aut/OXYFootballCycle.js
tests/
router port forwarding
public DNS
public IP exposure
/dev/nvme1n1
Wipe Disk
Initialize Disk with GPT
```

---

## 8. Completion criteria

OXY live stable checkpoint can be marked complete only if:

```text
1. http://192.168.1.252 responds.
2. nginx is active/running.
3. ssh is active/running.
4. index.html exists.
5. live directory listing is recorded.
6. backups are visible.
7. browser page loads.
8. Generator / Constructor / Hidden Editor remain separated.
9. No public access is configured.
10. GitHub docs are up to date.
```

---

## 9. What this checklist does not do

```text
Does not modify OXY.
Does not edit index.html.
Does not restart nginx.
Does not create backups.
Does not create VM101.
Does not download ISO.
Does not install AlmaLinux.
Does not install a panel.
Does not configure DNS.
Does not configure port forwarding.
```

---

## 10. Next safe stage after checklist

After this checklist is added and verified read-only:

```text
1. Run read-only live status checks manually.
2. Record the results in docs/OXY_LIVE_STABLE_STATUS.md.
3. Only after stable status is documented, continue AlmaLinux / VM101 install planning.
```

---

## 11. Final status

```text
OXY live stable checklist is documented.
No server changes were made.
No code changes were made.
VM100 remains protected.
VM101 remains not created.
AlmaLinux is not installed.
Panel is not installed.
Public access is not configured.
```