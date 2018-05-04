# <a name="class-mipprotectionprofile"></a>mip::ProtectionProfile, classe 
[ProtectionProfile](#classmip_1_1_protection_profile) est la classe racine utilisée pour effectuer des opérations de protection.
Une application doit créer un [ProtectionProfile](#classmip_1_1_protection_profile) avant d’effectuer des opérations de protection
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings & GetSettings public void ClearCaches | Supprime les caches (par exemple, bases de données de consentement, etc.)
## <a name="members"></a>Membres
### <a name="settings"></a>Paramètres
Obtient les paramètres utilisés par [ProtectionProfile](#classmip_1_1_protection_profile) lors de son initialisation et tout au long de sa durée de vie.
#### <a name="returns"></a>Returns
[Settings](#classmip_1_1_protection_profile_1_1_settings) utilisé par [ProtectionProfile](#classmip_1_1_protection_profile) lors de son initialisation et tout au long de sa durée de vie
### <a name="clearcaches"></a>ClearCaches
Supprime les caches (par exemple, bases de données de consentement, etc.) Utile pour le débogage et le test