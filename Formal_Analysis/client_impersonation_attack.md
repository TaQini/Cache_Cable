Process 0 (that is, the initial process):
{1}new victim_user: bitstring;
{2}new attacker_user: bitstring;
(
    {3}let C0: bitstring = victim_user in
    {4}new R1: bitstring;
    {5}new RS: bitstring;
    {6}let HS: bitstring = hash(RS) in
    {7}out(socket, (R1,HS));
    {8}let cable1: channel = funcG(R1,C0) in
    {9}out(cable1, RS);
    {10}in(socket, (R2: bitstring,HC: bitstring));
    {11}let cable2: channel = funcG(R2,C0) in
    {12}in(cable2, (RC: bitstring,C1: bitstring));
    {13}if (HC = hash(concat(RC,C1))) then
    {14}event ev1bpass;
    {15}new R3: bitstring;
    {16}let Csi: bitstring = funcE(Msi,RS) in
    {17}let Hsi: bitstring = hmac(RC,Csi) in
    {18}out(socket, (R3,Hsi));
    {19}let cable3: channel = funcG(R3,C1) in
    {20}out(cable3, Csi)
) | (
    {21}let C0_1: bitstring = attacker_user in
    {22}in(socket, (R1_1: bitstring,HS_1: bitstring));
    {23}let cable1_1: channel = funcG(R1_1,C0_1) in
    {24}in(cable1_1, RS_1: bitstring);
    {25}if (HS_1 = hash(RS_1)) then
    {26}event ev1apass;
    {27}new R2_1: bitstring;
    {28}new RC_1: bitstring;
    {29}new C1_1: bitstring;
    {30}let HC_1: bitstring = hash(concat(RC_1,C1_1)) in
    {31}out(socket, (R2_1,HC_1));
    {32}let cable2_1: channel = funcG(R2_1,C0_1) in
    {33}out(cable2_1, (RC_1,C1_1));
    {34}in(socket, (R3_1: bitstring,Hsi_1: bitstring));
    {35}let cable3_1: channel = funcG(R3_1,C1_1) in
    {36}in(cable3_1, Csi_1: bitstring);
    {37}if (Hsi_1 = hmac(RC_1,Csi_1)) then
    {38}event ev2pass;
    {39}let SI: bitstring = funcD(Csi_1,RS_1) in
    0
)

--  Process 1 (that is, process 0, with let moved downwards):
{1}new victim_user: bitstring;
{2}new attacker_user: bitstring;
(
    {4}new R1: bitstring;
    {5}new RS: bitstring;
    {6}let HS: bitstring = hash(RS) in
    {7}out(socket, (R1,HS));
    {3}let C0: bitstring = victim_user in
    {8}let cable1: channel = funcG(R1,C0) in
    {9}out(cable1, RS);
    {10}in(socket, (R2: bitstring,HC: bitstring));
    {11}let cable2: channel = funcG(R2,C0) in
    {12}in(cable2, (RC: bitstring,C1: bitstring));
    {13}if (HC = hash(concat(RC,C1))) then
    {14}event ev1bpass;
    {15}new R3: bitstring;
    {16}let Csi: bitstring = funcE(Msi,RS) in
    {17}let Hsi: bitstring = hmac(RC,Csi) in
    {18}out(socket, (R3,Hsi));
    {19}let cable3: channel = funcG(R3,C1) in
    {20}out(cable3, Csi)
) | (
    {22}in(socket, (R1_1: bitstring,HS_1: bitstring));
    {21}let C0_1: bitstring = attacker_user in
    {23}let cable1_1: channel = funcG(R1_1,C0_1) in
    {24}in(cable1_1, RS_1: bitstring);
    {25}if (HS_1 = hash(RS_1)) then
    {26}event ev1apass;
    {27}new R2_1: bitstring;
    {28}new RC_1: bitstring;
    {29}new C1_1: bitstring;
    {30}let HC_1: bitstring = hash(concat(RC_1,C1_1)) in
    {31}out(socket, (R2_1,HC_1));
    {32}let cable2_1: channel = funcG(R2_1,C0_1) in
    {33}out(cable2_1, (RC_1,C1_1));
    {34}in(socket, (R3_1: bitstring,Hsi_1: bitstring));
    {35}let cable3_1: channel = funcG(R3_1,C1_1) in
    {36}in(cable3_1, Csi_1: bitstring);
    {37}if (Hsi_1 = hmac(RC_1,Csi_1)) then
    {38}event ev2pass;
    {39}let SI: bitstring = funcD(Csi_1,RS_1) in
    0
)

-- Query not attacker(Msi[]) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,attacker_user[]),RS_2)/-5000
Starting query not attacker(Msi[])
RESULT not attacker(Msi[]) is true.
-- Query event(ev2pass) ==> event(ev1apass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,attacker_user[]),RS_2)/-5000
Starting query event(ev2pass) ==> event(ev1apass)
RESULT event(ev2pass) ==> event(ev1apass) is true.
-- Query event(ev2pass) ==> event(ev1bpass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,attacker_user[]),RS_2)/-5000
Starting query event(ev2pass) ==> event(ev1bpass)
RESULT event(ev2pass) ==> event(ev1bpass) is true.
-- Query not event(ev1apass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,attacker_user[]),RS_2)/-5000
Starting query not event(ev1apass)
RESULT not event(ev1apass) is true.
-- Query not event(ev1bpass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,attacker_user[]),RS_2)/-5000
Starting query not event(ev1bpass)
RESULT not event(ev1bpass) is true.
-- Query not event(ev2pass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,attacker_user[]),RS_2)/-5000
Starting query not event(ev2pass)
RESULT not event(ev2pass) is true.

--------------------------------------------------------------
Verification summary:

Query not attacker(Msi[]) is true.

Query event(ev2pass) ==> event(ev1apass) is true.

Query event(ev2pass) ==> event(ev1bpass) is true.

Query not event(ev1apass) is true.

Query not event(ev1bpass) is true.

Query not event(ev2pass) is true.

--------------------------------------------------------------

