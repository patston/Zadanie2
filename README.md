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


# Krok 2A


![](/2A_1.png)


![](/2B_1.png)


![](/2B_2.png)


![](/2B_3.png)


![](/3A_1.png)


![](/3A_2.png)


![](/3A_3.png)


![](/3A_4.png)


![](/3A_5.png)


![](/3B_1.png)


![](/3B_2.png)


![](/3B_3.png)


![](/4A_1.png)


![](/4A_2.png)


![](/4A_3.png)


![](/4A_4.png)


![](/4B_1.png)


![](/4B_2.png)


![](/4B_3.png)


![](/4B_4.png)


![](/4B_5.png)


![](/4B_6.png)

