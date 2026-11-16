# Lakshmi's Laundry

Laundry operations PWA connected to the Firebase project owned by
`naveenm0383@gmail.com`.

## Local run

```bash
python3 -m http.server 4173
```

Open `http://127.0.0.1:4173/` for the staff app and
`http://127.0.0.1:4173/customer.html` for customer pickup booking and order
tracking.

## Firebase

- Project ID: `lakshmi-s-laundry`
- Firestore region: `asia-south1` (Mumbai)
- Owner login: Google Sign-In with `naveenm0383@gmail.com`.
- Staff login: the owner adds the employee in **Masters → Staff & email
  access**, enters the employee's email, selects a role and permitted store,
  then switches on **Can use the staff app**. Staff can use Google Sign-In or
  verified email/password login. A temporary password is never stored in
  Firestore; the employee verifies the email and can use the password setup
  link to choose a private password.
- Roles: Admin, Store manager, Store staff (simple counter), Processing,
  and Rider. Admin has full operations for assigned stores, while only the
  owner can create or approve staff logins. Other staff see only the screens
  needed for their role.
- Customer page: public reads are limited to published store/tracking data;
  customers can create pickup requests.

The initial database includes one Hyderabad store, a Standard price list,
three services, two product groups, and five starter products. Review the
starter rates in **Masters → Product rates** before production use.

## Security and backup

- `firestore.rules` is the production authorization policy. The owner controls
  staff accounts; managers are limited to permitted stores; processing and
  rider accounts receive only their operational and personal pay data.
- Public customer tracking requires the bill number together with the order's
  mobile number. Mobile-only history and saved-address lookup are disabled.
  Public pickup requests accept only the expected fields with store, date,
  time-slot, length and mobile validation.
- Online pickup and UPI are intentionally off until the owner enters the real
  store mobile number, working pickup slots and UPI ID. Store managers start
  with a zero discount limit until the owner chooses a different limit.
- Use **Masters → Download full backup** regularly. Full backups contain
  transactions and payroll and must be stored privately.
- The Firebase Spark plan remains usable without a paid dependency. Email/
  password and Google providers must remain enabled in Firebase Authentication.

The deployment configuration is in `firebase.json`, and the Firebase project
alias is in `.firebaserc`.
