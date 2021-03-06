.. _tutorial-i:

=========================================
Tiwtorial I: Diffinio & Rhedeg Efelychiad
=========================================

Dychmygwch eich bod chi'n rheolwr banc, a hoffwch wybod pa mor hir mae cwsmeriaid yn aros yn y banc.
Mae cwsmeriaid yn cyrraedd ar hap, tua 12 yr awr, pryd bynnag amser o'r dydd yw hi.
Mae hyd wasanaeth ar hap, ond ar gyfartaledd yn para tua 10 munud.
Mae'r banc ar agor 24 awr y dydd, 7 diwrnod yr wythnos, ac mae ganddo 3 gweinydd sydd yn gweithio trwy'r amser.
Os yw pob gweinydd yn brysur, mae cwsmeriaid newydd yn aros mewn ciw ar gyfer gwasanaeth.
Ar gyfartaledd pa mor hir mae cwsmeriaid yn aros?

Fe allwn ni defnyddio efelychiad cyfrifiadurol i ffeindio mas.
Fan hyn byddwn yn efelychu'r system, hynny yw gwneud i'r cyfrifiadur esgus bod cwsmeriaid yn cyrraedd ac yn derbyn gwasanaeth yn y banc.
Yna allwn ni edrych ar yr holl gwsmeriaid rhith sy'n pasio trwy'r banc, i gael dealltwriaeth o sut mae'r system yn ymddwyn os bydd yn bodoli yn fywyd go iawn.

Dyma le mae Ciw yn ennill ei blwyf.
Gadewch i ni fewnbynnu Ciw::

    >>> import ciw

Nawr mae angen i ni ddweud wrth Ciw beth mae'r system yn edrych fel a sut mae'n ymddwyn.
Rydym yn gwneud hwn gan greu gwrthrych Network.
Mae'r cymryd mewn allweddeiriau sy'n cynnwys y wybodaeth ganlynol am y system:

+ Nifer o weinyddion (:code:`Number_of_servers`)
   + Faint o weinyddion sy'n gweithio yn y banc.
   + Yn yr achos yma, 3 gweinydd.

+ Dosraniad yr amseroedd rhwng-dyfodiad (:code:`Arrival_distributions`)
   + Dosraniad yr amseroedd rhwng dyfodiadau, rhwng cwsmeriaid olynol yn cyrraedd.
   + Yn yr achos yma bydd 12 yr awr yn golygu amser cymedrig o 5 munud rhwng dyfodiadau.

+ Dosraniad yr amseroedd gwasanaeth (:code:`Service_distributions`)
   + Dosraniad yr amseroedd mae'r cwsmeriaid yn gwario gyda gweinydd.
   + Yn yr achos yma amser cymedrig o 10 munud.

Ar gyfer y system bac, crëwch y Network::

    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(0.2)],
    ...     service_distributions=[ciw.dists.Exponential(0.1)],
    ...     number_of_servers=[3]
    ... )

Mae hwn yn disgrifio'r banc yn llawn.
Nodwch y dosraniadau; mae :code:`Exponential` yma yn golygu fod yr amseroedd gwasanaeth a rhwng-dyfodiad wedi deillio o `dosraniad esbonyddol <https://en.wikipedia.org/wiki/Exponential_distribution>`_.
Mae'r paramedrau :code:`0.2` a :code:`0.1` yn awgrymu amser cymedrig o 5 a 10 munud yn ôl eu trefn.
Felly mae'r gwrthrych Network yma yn diffinio'r system mewn munudau.

Yn gyntaf fe fyddwn yn :ref:`gosod hedyn <set-seed>`.
Mae hwn yn :ref:`ymarfer da <simulation-practice>`, a hefyd yn gwneud yn siŵr fod ein canlyniadau ac eich canlyniadau chi yn unfath:

    >>> ciw.seed(1)

Nawr fe allwn greu gwrthrych :code:`Simulation`.
Hwn fydd yr injan fydd yn rhedeg yr efelychiad:

    >>> Q = ciw.Simulation(N)

Gadewch i ni redeg yr efelychiad am un diwrnod o amser banc (paid â phoeni, ni fydd hwn yn cymryd un diwrnod o amser go iawn!).
Oherwydd diffinion ni'r system mewn munudau, fe fydd diwrnod yn cymryd 1440 unedau amser::

    >>> Q.simulate_until_max_time(1440)

Da iawn! Rydym ni nawr wedi diffinio ac efelychu banc am un diwrnod.
Yn y tiwtorial nesaf, fe fyddwn yn archwilio'r gwrthrych :code:`Simulation` rhagor.
