# Krok 1A

W tym kroku należało utworzyć repozytorium [SourceRepo](https://github.com/patston/SourceRepo). W tym repozytorium miały znajdować się pliki źródłowe aplikacji webowej.
Strona miała zawierać takie informacje jak: imię i nazwisko oraz numer wersji aplikacji. W SourceRepo miał znajdować się
również Dockerfile, który pozwala na zbudowanie obrazu Docker tej aplikacji.

Przed rozpoczęciem realizacji tego kroku zainstalowałem GitHub CLI za pomocą następującego polecenia:


![](/1A_1.png)


Następnie zalogowałem się na swoje konto GitHub (korzystając z GitHub CLI):


![](/1A_2.png)


![](/1A_3.png)


Później przeszedłem do realizacji kroku 1A. Utworzyłem prostą statyczną stronę, która wyświetla 
imię i nazwisko oraz wersję aplikacji:


![](/1A_4.png)


Następnie utworzyłem plik Dockerfile, który pozwala na zbudowanie obrazu Docker
powyżej przedstawionej strony webowej:


![](/1A_5.png)


Przy pomocy GitHub CLI utworzyłem repozytorium SourceRepo:


![](/1A_6.png)


Zrobiłem pierwszy commit i wykonałem push do repozytorium SourceRepo:


![](/1A_7.png)


![](/1A_8.png)


# Krok 1B

W tym kroku należało utworzyć repozytorium [ConfigRepo](https://github.com/patston/ConfigRepo). W tym repozytorium
miały znjadować się pliki manifestów yaml, które mają za zadanie utworzenie Deploymentu, Service typu NodePort oraz
Ingress.

Najpierw utworzyłem Deployment, na bazie opracowanego obrazu w kroku 1A. Deployment posiada 4 repliki,
dopuszcza w trakcie wykownywania aktualizacji jednoczesnej pracy maksymalnie 5 pod-ów w ramach aplikacji oraz
ogranicza minimalną liczbę działających podów do dwóch:


![](/1B_1.png)


Potem utworzyłęm usługę Service typu NodePort dla tej aplikacji:


![](/1B_2.png)


Następnie utworzyłem usługę dostępu zewnętrznego Ingress:


![](/1B_3.png)


Ostatecznie utworzyłem repozytorium ConfigRepo przy pomocy GitHub CLI:


![](/1B_4.png)


Zrobiłem pierwszy commit i wykonałem push do repozytorium ConfigRepo:


![](/1B_5.png)


# Krok 2A i 2B

W tych krokach należało w ramach repozytorium SourceRepo utworzyć plik .github/workflows/zad2lab10.yml, który
pozwoli na zbudowanie obrazu dla wybranych architektur sprzętowych (ang. mulWarch images), nadanie tag-u i 
przesłanie obrazu do swojego, publicznego repo na DockerHub oraz odpowiednią modyfikację manifestów yaml 
na repozytorium Config repo.

Najpierw utworzyłem katalog .github/workflows/


![](/2A_1.png)


Następnie utworzyłem plik zad2lab10.yml w powyższym katalogu. Zawiera on dwa zadania (ang. jobs), czyli dockerCI i
kubernetesCI. 
DockerCI wykorzystuje następujące moduły actions, które są dostępnie w systemie action marketplace:
- actions/checkout - skojarzenie workflow z SourceRepo,
- docker/setup-qemu-action - instalacja QEMU,
- docker/setup-buildxaction - instalacja silnika budowy obrazów Buildx,
- docker/login-action - logowanie na koncie DockerHub,
- docker/build-push-action - budowę obrazu Docker dla architektur amd64 oraz arm64, nadanie właściwej
nazwy obrazu i przesłanie tego wieloarchitekturowego obrazu na wskazanekonto na DockerHub.

Do zalogowania się na DockerHub wykorzystałem Actions secrets dla repozytorium SourceRepo. Warto wspomnieć, że
GitHub Actions workflow wykorzystuje najnowszą wersję systemu Ubuntu oraz pozwala na uruchomienie na podstawie
decyzji użytkownika (workflow_dispatch). Dodatkowo wykorzystałem inputs.tag, dzięki czemu podczas uruchamiania
tego workflow, zostaniemy poproszeni o podanie wersji aplikacji.


![](/2B_1.png)


KubernetesCI modyfikuje zawartość manifestów w ConfigRepo, tak aby zawierał nowy obraz Docker (nową wersję aplikacji).
Wykorzystuje w tym celu edytor sed. Ten job również zawiera skojarzenie z repozytorium, tym razem z ConfigRepo.
Tutaj również skorzystałem z Actions secrets, aby podać token do repozytorium ConfigRepo.


![](/2B_2.png)


Ostatecznie wykonałem push do repozytorium SourceRepo:


![](/2B_3.png)


# Krok 3A

W tym kroku należało opracować obraz o nazwie [zad2gitops](https://hub.docker.com/r/patston/zad2gitops).
Obraz bazuje na najnowszej wersji systemu alpine oraz zawiera git, curl oraz kubectl.
Plik Dockerfile został przedstawiony poniżej:


![](/3A_1.png)


Następnie zbudowałem ten obraz:


![](/3A_2.png)


Zalogowałem się na DockerHub i wykonałem push tego obrazu:


![](/3A_3.png)


Ostatecznie wykonałem push tego pliku Dockerfile do SourceRepo:


![](/3A_4.png)


Obraz [zad2gitops](https://hub.docker.com/r/patston/zad2gitops) na DockerHub:


![](/3A_5.png)


# Krok 3B

W tym koroku należało utworzyć manifest obiektu CronJob o nazwie stepcd, który ma co dwie minuty klonować
zawartość repozytorium ConfigRepo do katalagu tymczasowgo (u mnie /tmp) w systemie plików kontenera. Również
ma za zadanie co dwie minuty uruchamiać manifesty, które znajdują się w katalogu /tmp, a więc w ten sposób
inicjalizuje proces aktualizacji. Aktualizacja realizowana jest z uprawnieniami konta gitops.

Poniżej znajduje się manifest obiektu CronJob o nazwie stepcd:


![](/3B_1.png)


Następnie przed uruchomieniem powyższego CronJob'a wykonałem poniższe polecenia:


![](/3B_2.png)


Następnie uruchomiłem CronJob'a przy pomocy poniższego polecenia:


![](/3B_3.png)


# Krok 4A

W tym kroku należało sprawdzić czy opracowana aplikacja jest dostępna z zewnątrz klastra Minikube, wykorzystując skonfigurowany
zasób Ingress.

Najpierw uruchomiłem minikube tunnel:


![](/4A_1.png)


Później sprawdziłem poprawność konfiguracji Ingress:


![](/4A_2.png)


Następnie dodałem wpis w /etc/hosts


![](/4A_3.png)


Wynik http://zad2.lab:


![](/4A_4.png)


# Krok 4B:




![](/4B_1.png)


![](/4B_2.png)


![](/4B_3.png)


![](/4B_4.png)


![](/4B_5.png)


![](/4B_6.png)

