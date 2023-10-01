# THM-Cheat-Sheet-
Zbiór zasobów i przydatnych polecen:

1. [Bash](#bash)
   1. [Pozostaw Bash bez historii](#bash-no-history)
   1. [Ukryj swoje polecenia](#bash-hide-command)

<a id="bash"></a>
# BASH


<a id="bash-no-history"></a>
## 1. Pozostaw Bash bez historii
Zmiana ustawiń powłoki Bash, aby używał */dev/null* zamiast *~/.bash_history*. Jest to pierwsze polecenie, które wykonujemy w każdej powłoce. Zatrzyma ono rejestrowanie poleceń przez Bash.
(Czyścimy również zmienne SSH_* na wypadek, gdybyśmy zalogowali się przez SSH. W przeciwnym razie każdy uruchomiony przez nas proces otrzyma kopię naszego IP w /proc/self/environ).
```sh
export HISTFILE=/dev/null
unset SSH_CONNECTION SSH_CLIENT
```
Dobrą praktyką jest "zabice wszystkich procc" podczas wychodzenia z powłoki:
```sh
alias exit='kill -9 $$'
```
Każde polecenie zaczynające się od " " (spacja) [nie zostanie zapisane w historii].
```
$  id
```
<a id="bash-hide-command"></a>
## 2 Ukryj swoje polecenial
