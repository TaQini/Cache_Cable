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
    {21}let C0_1: bitstring = victim_user in
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
    {21}let C0_1: bitstring = victim_user in
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
select mess(funcG(R1_2,victim_user[]),RS_2)/-5000
Starting query not attacker(Msi[])
RESULT not attacker(Msi[]) is true.
-- Query event(ev2pass) ==> event(ev1apass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,victim_user[]),RS_2)/-5000
Starting query event(ev2pass) ==> event(ev1apass)
goal reachable: b-event(ev1apass) -> event(ev2pass)
RESULT event(ev2pass) ==> event(ev1apass) is true.
-- Query event(ev2pass) ==> event(ev1bpass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,victim_user[]),RS_2)/-5000
Starting query event(ev2pass) ==> event(ev1bpass)
goal reachable: b-event(ev1bpass) -> event(ev2pass)
RESULT event(ev2pass) ==> event(ev1bpass) is true.
-- Query not event(ev1apass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,victim_user[]),RS_2)/-5000
Starting query not event(ev1apass)
goal reachable: event(ev1apass)

Derivation:

1. The message (R1[],hash(RS[])) may be sent to the attacker at output {7}.
attacker((R1[],hash(RS[]))).

2. By 1, the attacker may know (R1[],hash(RS[])).
Using the function 2-proj-2-tuple the attacker may obtain hash(RS[]).
attacker(hash(RS[])).

3. By 1, the attacker may know (R1[],hash(RS[])).
Using the function 1-proj-2-tuple the attacker may obtain R1[].
attacker(R1[]).

4. By 3, the attacker may know R1[].
By 2, the attacker may know hash(RS[]).
Using the function 2-tuple the attacker may obtain (R1[],hash(RS[])).
attacker((R1[],hash(RS[]))).

5. The message RS[] may be sent on channel funcG(R1[],victim_user[]) at output {9}.
mess(funcG(R1[],victim_user[]),RS[]).

6. The message (R1[],hash(RS[])) that the attacker may have by 4 may be received at input {22}.
The message RS[] that may be sent on channel funcG(R1[],victim_user[]) by 5 may be received at input {24}.
So event ev1apass may be executed at {26}.
event(ev1apass).

7. By 6, event(ev1apass).
The goal is reached, represented in the following fact:
event(ev1apass).


A more detailed output of the traces is available with
  set traceDisplay = long.

new victim_user: bitstring creating victim_user_1 at {1}

new attacker_user: bitstring creating attacker_user_1 at {2}

new R1: bitstring creating R1_2 at {4}

new RS: bitstring creating RS_2 at {5}

out(socket, (~M,~M_1)) with ~M = R1_2, ~M_1 = hash(RS_2) at {7}

in(socket, (~M,~M_1)) with ~M = R1_2, ~M_1 = hash(RS_2) at {22}

out(funcG(R1_2,victim_user_1), RS_2) at {9} received at {24}

event ev1apass at {26} (goal)

The event ev1apass is executed at {26}.
A trace has been found.
RESULT not event(ev1apass) is false.
-- Query not event(ev1bpass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,victim_user[]),RS_2)/-5000
Starting query not event(ev1bpass)
goal reachable: event(ev1bpass)

Derivation:
Abbreviations:
R2_2 = R2_1[RS_1 = RS[],HS_1 = hash(RS[]),R1_1 = R1[]]
RC_2 = RC_1[RS_1 = RS[],HS_1 = hash(RS[]),R1_1 = R1[]]
C1_2 = C1_1[RS_1 = RS[],HS_1 = hash(RS[]),R1_1 = R1[]]

1. The message (R1[],hash(RS[])) may be sent to the attacker at output {7}.
attacker((R1[],hash(RS[]))).

2. By 1, the attacker may know (R1[],hash(RS[])).
Using the function 2-proj-2-tuple the attacker may obtain hash(RS[]).
attacker(hash(RS[])).

3. By 1, the attacker may know (R1[],hash(RS[])).
Using the function 1-proj-2-tuple the attacker may obtain R1[].
attacker(R1[]).

4. By 3, the attacker may know R1[].
By 2, the attacker may know hash(RS[]).
Using the function 2-tuple the attacker may obtain (R1[],hash(RS[])).
attacker((R1[],hash(RS[]))).

5. The message RS[] may be sent on channel funcG(R1[],victim_user[]) at output {9}.
mess(funcG(R1[],victim_user[]),RS[]).

6. The message (R1[],hash(RS[])) that the attacker may have by 4 may be received at input {22}.
The message RS[] that may be sent on channel funcG(R1[],victim_user[]) by 5 may be received at input {24}.
So the message (R2_2,hash(concat(RC_2,C1_2))) may be sent to the attacker at output {31}.
attacker((R2_2,hash(concat(RC_2,C1_2)))).

7. By 6, the attacker may know (R2_2,hash(concat(RC_2,C1_2))).
Using the function 2-proj-2-tuple the attacker may obtain hash(concat(RC_2,C1_2)).
attacker(hash(concat(RC_2,C1_2))).

8. By 6, the attacker may know (R2_2,hash(concat(RC_2,C1_2))).
Using the function 1-proj-2-tuple the attacker may obtain R2_2.
attacker(R2_2).

9. By 8, the attacker may know R2_2.
By 7, the attacker may know hash(concat(RC_2,C1_2)).
Using the function 2-tuple the attacker may obtain (R2_2,hash(concat(RC_2,C1_2))).
attacker((R2_2,hash(concat(RC_2,C1_2)))).

10. The message (R1[],hash(RS[])) that the attacker may have by 4 may be received at input {22}.
The message RS[] that may be sent on channel funcG(R1[],victim_user[]) by 5 may be received at input {24}.
So the message (RC_2,C1_2) may be sent on channel funcG(R2_2,victim_user[]) at output {33}.
mess(funcG(R2_2,victim_user[]),(RC_2,C1_2)).

11. The message (R2_2,hash(concat(RC_2,C1_2))) that the attacker may have by 9 may be received at input {10}.
The message (RC_2,C1_2) that may be sent on channel funcG(R2_2,victim_user[]) by 10 may be received at input {12}.
So event ev1bpass may be executed at {14}.
event(ev1bpass).

12. By 11, event(ev1bpass).
The goal is reached, represented in the following fact:
event(ev1bpass).


A more detailed output of the traces is available with
  set traceDisplay = long.

new victim_user: bitstring creating victim_user_1 at {1}

new attacker_user: bitstring creating attacker_user_1 at {2}

new R1: bitstring creating R1_2 at {4}

new RS: bitstring creating RS_2 at {5}

out(socket, (~M,~M_1)) with ~M = R1_2, ~M_1 = hash(RS_2) at {7}

in(socket, (~M,~M_1)) with ~M = R1_2, ~M_1 = hash(RS_2) at {22}

out(funcG(R1_2,victim_user_1), RS_2) at {9} received at {24}

event ev1apass at {26}

new R2_1: bitstring creating R2_3 at {27}

new RC_1: bitstring creating RC_3 at {28}

new C1_1: bitstring creating C1_3 at {29}

out(socket, (~M_2,~M_3)) with ~M_2 = R2_3, ~M_3 = hash(concat(RC_3,C1_3)) at {31}

in(socket, (~M_2,~M_3)) with ~M_2 = R2_3, ~M_3 = hash(concat(RC_3,C1_3)) at {10}

out(funcG(R2_3,victim_user_1), (RC_3,C1_3)) at {33} received at {12}

event ev1bpass at {14} (goal)

The event ev1bpass is executed at {14}.
A trace has been found.
RESULT not event(ev1bpass) is false.
-- Query not event(ev2pass) in process 1.
Translating the process into Horn clauses...
Completing...
select mess(funcG(R1_2,victim_user[]),RS_2)/-5000
Starting query not event(ev2pass)
goal reachable: event(ev2pass)

Derivation:
Abbreviations:
C1_2 = C1_1[RS_1 = RS[],HS_1 = hash(RS[]),R1_1 = R1[]]
RC_2 = RC_1[RS_1 = RS[],HS_1 = hash(RS[]),R1_1 = R1[]]
R2_2 = R2_1[RS_1 = RS[],HS_1 = hash(RS[]),R1_1 = R1[]]
R3_2 = R3[C1 = C1_2,RC = RC_2,HC = hash(concat(RC_2,C1_2)),R2 = R2_2]

1. The message (R1[],hash(RS[])) may be sent to the attacker at output {7}.
attacker((R1[],hash(RS[]))).

2. By 1, the attacker may know (R1[],hash(RS[])).
Using the function 2-proj-2-tuple the attacker may obtain hash(RS[]).
attacker(hash(RS[])).

3. By 1, the attacker may know (R1[],hash(RS[])).
Using the function 1-proj-2-tuple the attacker may obtain R1[].
attacker(R1[]).

4. By 3, the attacker may know R1[].
By 2, the attacker may know hash(RS[]).
Using the function 2-tuple the attacker may obtain (R1[],hash(RS[])).
attacker((R1[],hash(RS[]))).

5. The message RS[] may be sent on channel funcG(R1[],victim_user[]) at output {9}.
mess(funcG(R1[],victim_user[]),RS[]).

6. The message (R1[],hash(RS[])) that the attacker may have by 4 may be received at input {22}.
The message RS[] that may be sent on channel funcG(R1[],victim_user[]) by 5 may be received at input {24}.
So the message (R2_2,hash(concat(RC_2,C1_2))) may be sent to the attacker at output {31}.
attacker((R2_2,hash(concat(RC_2,C1_2)))).

7. By 6, the attacker may know (R2_2,hash(concat(RC_2,C1_2))).
Using the function 2-proj-2-tuple the attacker may obtain hash(concat(RC_2,C1_2)).
attacker(hash(concat(RC_2,C1_2))).

8. By 6, the attacker may know (R2_2,hash(concat(RC_2,C1_2))).
Using the function 1-proj-2-tuple the attacker may obtain R2_2.
attacker(R2_2).

9. By 8, the attacker may know R2_2.
By 7, the attacker may know hash(concat(RC_2,C1_2)).
Using the function 2-tuple the attacker may obtain (R2_2,hash(concat(RC_2,C1_2))).
attacker((R2_2,hash(concat(RC_2,C1_2)))).

10. The message (R1[],hash(RS[])) that the attacker may have by 4 may be received at input {22}.
The message RS[] that may be sent on channel funcG(R1[],victim_user[]) by 5 may be received at input {24}.
So the message (RC_2,C1_2) may be sent on channel funcG(R2_2,victim_user[]) at output {33}.
mess(funcG(R2_2,victim_user[]),(RC_2,C1_2)).

11. The message (R2_2,hash(concat(RC_2,C1_2))) that the attacker may have by 9 may be received at input {10}.
The message (RC_2,C1_2) that may be sent on channel funcG(R2_2,victim_user[]) by 10 may be received at input {12}.
So the message (R3_2,hmac(RC_2,funcE(Msi[],RS[]))) may be sent to the attacker at output {18}.
attacker((R3_2,hmac(RC_2,funcE(Msi[],RS[])))).

12. By 11, the attacker may know (R3_2,hmac(RC_2,funcE(Msi[],RS[]))).
Using the function 2-proj-2-tuple the attacker may obtain hmac(RC_2,funcE(Msi[],RS[])).
attacker(hmac(RC_2,funcE(Msi[],RS[]))).

13. By 11, the attacker may know (R3_2,hmac(RC_2,funcE(Msi[],RS[]))).
Using the function 1-proj-2-tuple the attacker may obtain R3_2.
attacker(R3_2).

14. By 13, the attacker may know R3_2.
By 12, the attacker may know hmac(RC_2,funcE(Msi[],RS[])).
Using the function 2-tuple the attacker may obtain (R3_2,hmac(RC_2,funcE(Msi[],RS[]))).
attacker((R3_2,hmac(RC_2,funcE(Msi[],RS[])))).

15. The message (R2_2,hash(concat(RC_2,C1_2))) that the attacker may have by 9 may be received at input {10}.
The message (RC_2,C1_2) that may be sent on channel funcG(R2_2,victim_user[]) by 10 may be received at input {12}.
So the message funcE(Msi[],RS[]) may be sent on channel funcG(R3_2,C1_2) at output {20}.
mess(funcG(R3_2,C1_2),funcE(Msi[],RS[])).

16. The message (R1[],hash(RS[])) that the attacker may have by 4 may be received at input {22}.
The message RS[] that may be sent on channel funcG(R1[],victim_user[]) by 5 may be received at input {24}.
The message (R3_2,hmac(RC_2,funcE(Msi[],RS[]))) that the attacker may have by 14 may be received at input {34}.
The message funcE(Msi[],RS[]) that may be sent on channel funcG(R3_2,C1_2) by 15 may be received at input {36}.
So event ev2pass may be executed at {38}.
event(ev2pass).

17. By 16, event(ev2pass).
The goal is reached, represented in the following fact:
event(ev2pass).


A more detailed output of the traces is available with
  set traceDisplay = long.

new victim_user: bitstring creating victim_user_1 at {1}

new attacker_user: bitstring creating attacker_user_1 at {2}

new R1: bitstring creating R1_2 at {4}

new RS: bitstring creating RS_2 at {5}

out(socket, (~M,~M_1)) with ~M = R1_2, ~M_1 = hash(RS_2) at {7}

in(socket, (~M,~M_1)) with ~M = R1_2, ~M_1 = hash(RS_2) at {22}

out(funcG(R1_2,victim_user_1), RS_2) at {9} received at {24}

event ev1apass at {26}

new R2_1: bitstring creating R2_3 at {27}

new RC_1: bitstring creating RC_3 at {28}

new C1_1: bitstring creating C1_3 at {29}

out(socket, (~M_2,~M_3)) with ~M_2 = R2_3, ~M_3 = hash(concat(RC_3,C1_3)) at {31}

in(socket, (~M_2,~M_3)) with ~M_2 = R2_3, ~M_3 = hash(concat(RC_3,C1_3)) at {10}

out(funcG(R2_3,victim_user_1), (RC_3,C1_3)) at {33} received at {12}

event ev1bpass at {14}

new R3: bitstring creating R3_3 at {15}

out(socket, (~M_4,~M_5)) with ~M_4 = R3_3, ~M_5 = hmac(RC_3,funcE(Msi,RS_2)) at {18}

in(socket, (~M_4,~M_5)) with ~M_4 = R3_3, ~M_5 = hmac(RC_3,funcE(Msi,RS_2)) at {34}

out(funcG(R3_3,C1_3), funcE(Msi,RS_2)) at {20} received at {36}

event ev2pass at {38} (goal)

The event ev2pass is executed at {38}.
A trace has been found.
RESULT not event(ev2pass) is false.

--------------------------------------------------------------
Verification summary:

Query not attacker(Msi[]) is true.

Query event(ev2pass) ==> event(ev1apass) is true.

Query event(ev2pass) ==> event(ev1bpass) is true.

Query not event(ev1apass) is false.

Query not event(ev1bpass) is false.

Query not event(ev2pass) is false.

--------------------------------------------------------------

