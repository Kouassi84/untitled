# untitled
Mini-projet Symfony2 ( Gestion d'un aeroport )

ANALYSE DES BESIONS :
Cette démarche d’étude permet à identifier les besoins de notre application
Durant cette étude on a pu identifier les besoins suivants :
Gérer les Réservations.
Gérer l’organisation de vols.
Gérer les avions.
Gérer les Passagers.
Gérer les pilotes.
//on peut aussi gerer les reservations, les lignes, les classes ect
LES TABLES :

Chaque Pilote  est caractérisé par :
 id ,marticule, nom, prénom, nationalité, adresse et N°Téléphone.
Chaque Vol est caractérisé par :
Nom,numero, date de départ et l’heure d’arrivé,date de creation.
Chaque Avion est caractérisé par :
N°avion, Nom et capacité et la date de premiere circulation.

//2 tables de jointures entre Passager et vol et entre pilote et vol
table Resrvation, table affecter
LES CARDINALITES:
Un pilote peut être affecter de 1,n  vol
Un vol peut être affecter de 1,n pilote} on a une relation ManyToMany 

Un passager peut réserver  dans 1, n vol}on a une relation ManyToMany 
Un vol peut avoir 1, n réservation

Un avion effectue 1, n vol
Un vol effectue par 1,1 avion
//ON PEUT AVOIR D'autre relations comme des avions et les lignes les passagers et les classes  ect
outil utilisé
SYMFON2
-FOUSuserBundle  +>GESTION DES DROITS des membres
-sonataAdminBundle > creation d'une administration cle en main
-knpgeneratorBundle > gestion de la pagination,
-FixtureBundle >pour nos donnees de developpement
Developpement
le code peut etre vraiment amelioré c'est juste une petit ebauche 
PERMISSIONS exemple
-permission =>PASSAGER =>ROLE_PASSAGER   { MOT de passe = 123456, nom utilisateur = azale }
-permisson =>pilote =>ROLE_PILOTE  { MOT de passe = 123456, nom utilisateur = adil }
->permisson =>gestionnaire= ROLE_GESTIONNAIRE { MOT de passe = 123456, nom utilisateur = gestionnaire }
->permission=>super_admin=> ROLE_SUPER_ADMIN  { MOT de passe = 123456, nom utilisateur = admin }

<!-------------------------CE QUE NOUS POUVONT RAJOUTER--------------------------------------------------->
-pour les formulaires de la genstions des passagers des pilotes ON PEUT UTILISER l'imbrication de formulaire 
 pour rendre encore plus optimal le developpement
- on peut mettre des contrainte de gestion sur les passagers et le pilote
-creer des eventlistner pour rendre certaines tâches automatique a cela creer des services ect
-utliser un editeur comme CkeDITOR 
<!--------------------------------CE QUI A ETE FAIT-------------------------------->
-gestion de l'espace membre connection,inscription,mot de passe perdu regeneration de mode passe 
-bundle FOSuserBundle
-gestion de l'adminstration avec le bundle sonataAdminBundle avec un simple comfiguration 
->on peut lister les passagers
->peut lister les pilotes
->on peut lister les avions et les vols
sur la page d'acceuil on a un tri de vol au depart de marseille et a destination de marseille qui peut etre amelioré
-creation de deux bundle
-le bundle PagesBundle pour gerer mes pages 
-le bundle KF qui est le bundle du mini projet
-utilisation de bootstrap pour avoir une vue agreable
-utilisation des fixtures pour remplir ma base de donnée

 <!--- creation de la base de donneé-->
 
 -- phpMyAdmin SQL Dump
-- version 4.1.14
-- http://www.phpmyadmin.net
--
-- Client :  127.0.0.1
-- Généré le :  Jeu 22 Octobre 2015 à 14:18
-- Version du serveur :  5.6.17
-- Version de PHP :  5.5.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;

--
-- Base de données :  `untitled`
--

-- --------------------------------------------------------

--
-- Structure de la table `affecter`
--

CREATE TABLE IF NOT EXISTS `affecter` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `pilote_id` int(11) DEFAULT NULL,
  `vol_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `IDX_3BE6672CF510AAE9` (`pilote_id`),
  KEY `IDX_3BE6672C9F2BFB7A` (`vol_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=4 ;

--
-- Contenu de la table `affecter`
--

INSERT INTO `affecter` (`id`, `pilote_id`, `vol_id`) VALUES
(1, NULL, NULL),
(2, NULL, NULL),
(3, NULL, NULL);

-- --------------------------------------------------------

--
-- Structure de la table `avion`
--

CREATE TABLE IF NOT EXISTS `avion` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `vol_id` int(11) DEFAULT NULL,
  `nom` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `capacite` int(11) NOT NULL,
  `date_circulation` datetime NOT NULL,
  PRIMARY KEY (`id`),
  KEY `IDX_234D9D389F2BFB7A` (`vol_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=3 ;

--
-- Contenu de la table `avion`
--

INSERT INTO `avion` (`id`, `vol_id`, `nom`, `capacite`, `date_circulation`) VALUES
(1, 3, 'Air-bus 300', 450, '1980-11-19 00:00:00'),
(2, 4, 'Airbus a320', 750, '1990-10-13 00:00:00');

-- --------------------------------------------------------

--
-- Structure de la table `pages`
--

CREATE TABLE IF NOT EXISTS `pages` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `titre` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `contenu` longtext COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=3 ;

--
-- Contenu de la table `pages`
--

INSERT INTO `pages` (`id`, `titre`, `contenu`) VALUES
(1, 'CGV', '\n            <div class="row">\n                <h4>Item Brand and Category</h4>\n                <h5>AB29837 Item Model</h5>\n                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry ''s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>\n            </div>\n            <div class="row">\n                <h4>Item Brand and Category</h4>\n                <h5>AB29837 Item Model</h5>\n                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry''s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>\n            </div>\n            <div class="row">\n                <h4>Item Brand and Category</h4>\n                <h5>AB29837 Item Model</h5>\n                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry''s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>\n            </div>'),
(2, 'Mentions légales', '<div class="row">\n                <h4>Item Brand and Category</h4>\n                <h5>AB29837 Item Model</h5>\n                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry ''s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>\n            </div>\n            <div class="row">\n                <h4>Item Brand and Category</h4>\n                <h5>AB29837 Item Model</h5>\n                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry''s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>\n            </div>\n            <div class="row">\n                <h4>Item Brand and Category</h4>\n                <h5>AB29837 Item Model</h5>\n                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry''s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>\n            </div>');

-- --------------------------------------------------------

--
-- Structure de la table `passager`
--

CREATE TABLE IF NOT EXISTS `passager` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nom` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `prenom` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `naissance` datetime NOT NULL,
  `Nationalite` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `localite` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `attribution` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=6 ;

--
-- Contenu de la table `passager`
--

INSERT INTO `passager` (`id`, `nom`, `prenom`, `naissance`, `Nationalite`, `localite`, `attribution`) VALUES
(1, 'azale', 'francky', '1997-11-13 00:00:00', 'CY', 'caracasse', ''),
(2, 'zenaby', 'bakadjy', '1996-11-17 00:00:00', 'SI', 'marseille', ''),
(3, 'Margarette', 'valerienne', '1982-07-16 00:00:00', 'BO', 'carpentras', ''),
(4, 'Mikity', 'rolle', '1989-05-19 00:00:00', 'DE', 'berlin', ''),
(5, 'bernadette', 'isla', '1990-05-18 00:00:00', 'VE', 'rome', '');

-- --------------------------------------------------------

--
-- Structure de la table `pilote`
--

CREATE TABLE IF NOT EXISTS `pilote` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nom` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `prenom` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `matricule` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `birthday` datetime NOT NULL,
  `adresse` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `telephone` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `affectation` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=4 ;

--
-- Contenu de la table `pilote`
--

INSERT INTO `pilote` (`id`, `nom`, `prenom`, `matricule`, `birthday`, `adresse`, `telephone`, `affectation`) VALUES
(1, 'adil', 'haouche', '12345678', '1989-05-16 00:00:00', 'casablanca', '0645781278', ''),
(2, 'Margaritta', 'benedicte', '7841235689', '1977-06-17 00:00:00', 'miami', '0245789623', ''),
(3, 'jakarta', 'rachid', '123456', '1915-09-15 00:00:00', 'seoul', '0123456987', '');

-- --------------------------------------------------------

--
-- Structure de la table `reservation`
--

CREATE TABLE IF NOT EXISTS `reservation` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `passager_id` int(11) DEFAULT NULL,
  `vol_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `IDX_C454C68271A51189` (`passager_id`),
  KEY `IDX_C454C6829F2BFB7A` (`vol_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=3 ;

--
-- Contenu de la table `reservation`
--

INSERT INTO `reservation` (`id`, `passager_id`, `vol_id`) VALUES
(1, 1, 1),
(2, 2, 1);

-- --------------------------------------------------------

--
-- Structure de la table `user`
--

CREATE TABLE IF NOT EXISTS `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `username_canonical` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `email` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `email_canonical` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `enabled` tinyint(1) NOT NULL,
  `salt` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `password` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `last_login` datetime DEFAULT NULL,
  `locked` tinyint(1) NOT NULL,
  `expired` tinyint(1) NOT NULL,
  `expires_at` datetime DEFAULT NULL,
  `confirmation_token` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
  `password_requested_at` datetime DEFAULT NULL,
  `roles` longtext COLLATE utf8_unicode_ci NOT NULL COMMENT '(DC2Type:array)',
  `credentials_expired` tinyint(1) NOT NULL,
  `credentials_expire_at` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `UNIQ_2DA1797792FC23A8` (`username_canonical`),
  UNIQUE KEY `UNIQ_2DA17977A0D96FBF` (`email_canonical`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=6 ;

--
-- Contenu de la table `user`
--

INSERT INTO `user` (`id`, `username`, `username_canonical`, `email`, `email_canonical`, `enabled`, `salt`, `password`, `last_login`, `locked`, `expired`, `expires_at`, `confirmation_token`, `password_requested_at`, `roles`, `credentials_expired`, `credentials_expire_at`) VALUES
(2, 'azale', 'azale', 'azale@yopmail.com', 'azale@yopmail.com', 1, 'hmbxx07rulcgwggsw0ws40cccs8s0cg', '$2y$13$hmbxx07rulcgwggsw0ws4uj0UwtEPVh0FH9UcDB.bWFwTGRA/JfTS', '2015-10-22 14:01:52', 0, 0, NULL, NULL, NULL, 'a:1:{i:0;s:13:"ROLE_PASSAGER";}', 0, NULL),
(3, 'admin', 'admin', 'admin@yopmail.com', 'admin@yopmail.com', 1, 'fvvgrn3jrp4wg00ggsc0ssogogsswws', '$2y$13$fvvgrn3jrp4wg00ggsc0sekHp.vrfOVHtrsNN228cEEdVid/FISjm', '2015-10-22 11:14:55', 0, 0, NULL, NULL, NULL, 'a:1:{i:0;s:16:"ROLE_SUPER_ADMIN";}', 0, NULL),
(4, 'adil', 'adil', 'adil@yopmail.com', 'adil@yopmail.com', 1, 'hqsr7defne0owk48w8c8ks4o0cgkoks', '$2y$13$hqsr7defne0owk48w8c8kev.BchiVoSqKelCMlACUln7JdcWpcgNu', '2015-10-21 20:11:47', 0, 0, NULL, NULL, NULL, 'a:1:{i:0;s:11:"ROLE_PILOTE";}', 0, NULL),
(5, 'gestionnaire', 'gestionnaire', 'gestionnaire@yopmail.com', 'gestionnaire@yopmail.com', 1, 'c9shh5sbtnccw88kwg84s00cw808848', '$2y$13$c9shh5sbtnccw88kwg84sucTNk4Be19qFozJ3E/tCkQW/wkUZIK46', '2015-10-22 12:32:01', 0, 0, NULL, NULL, NULL, 'a:1:{i:0;s:10:"ROLE_ADMIN";}', 0, NULL);

-- --------------------------------------------------------

--
-- Structure de la table `vol`
--

CREATE TABLE IF NOT EXISTS `vol` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nom` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `numero` int(11) NOT NULL,
  `heure_depart` datetime NOT NULL,
  `heure_arrivee` datetime NOT NULL,
  `created_at` datetime NOT NULL,
  `depart` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `arrivee` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=5 ;

--
-- Contenu de la table `vol`
--

INSERT INTO `vol` (`id`, `nom`, `numero`, `heure_depart`, `heure_arrivee`, `created_at`, `depart`, `arrivee`) VALUES
(1, 'azerty 456', 123456, '2015-10-21 21:30:00', '2015-10-20 22:00:00', '2015-10-21 19:23:00', 'Marseille', 'Rome'),
(2, 'azf589', 985231, '2015-10-21 19:33:00', '2015-10-20 22:00:00', '2015-10-21 19:33:00', 'Marseille', 'Bruxelle'),
(3, 'kGG 45689', 85236, '2015-10-21 19:35:00', '2015-10-21 21:00:00', '2015-10-21 19:35:00', 'Marseille', 'Madrid'),
(4, 'wo789456', 12345829, '2015-10-21 19:36:00', '2015-10-21 22:17:00', '2015-10-21 19:36:00', 'Marseille', 'Berlin');

--
-- Contraintes pour les tables exportées
--

--
-- Contraintes pour la table `affecter`
--
ALTER TABLE `affecter`
  ADD CONSTRAINT `FK_3BE6672C9F2BFB7A` FOREIGN KEY (`vol_id`) REFERENCES `vol` (`id`),
  ADD CONSTRAINT `FK_3BE6672CF510AAE9` FOREIGN KEY (`pilote_id`) REFERENCES `pilote` (`id`);

--
-- Contraintes pour la table `avion`
--
ALTER TABLE `avion`
  ADD CONSTRAINT `FK_234D9D389F2BFB7A` FOREIGN KEY (`vol_id`) REFERENCES `vol` (`id`);

--
-- Contraintes pour la table `reservation`
--
ALTER TABLE `reservation`
  ADD CONSTRAINT `FK_C454C68271A51189` FOREIGN KEY (`passager_id`) REFERENCES `passager` (`id`),
  ADD CONSTRAINT `FK_C454C6829F2BFB7A` FOREIGN KEY (`vol_id`) REFERENCES `vol` (`id`);

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;





