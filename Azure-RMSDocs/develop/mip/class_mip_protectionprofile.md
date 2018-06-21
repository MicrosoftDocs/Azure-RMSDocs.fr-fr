# <a name="class-mipprotectionprofile"></a>mip::ProtectionProfile, classe 
[ProtectionProfile](class_mip_protectionprofile.md) est la classe racine utilisée pour effectuer des opérations de protection.
Une application doit créer un [ProtectionProfile](class_mip_protectionprofile.md) avant d’effectuer des opérations de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtient les paramètres utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie.
 public void ClearCaches()  |  Supprime les caches (par exemple, bases de données de consentement, etc.)
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtient les paramètres utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie.

  
**Retourne** : les [paramètres](class_mip_protectionprofile_settings.md) utilisés par [ProtectionProfile](class_mip_protectionprofile.md) lors de son initialisation et tout au long de sa durée de vie
  
### <a name="clearcaches"></a>ClearCaches
Supprime les caches (par exemple, bases de données de consentement, etc.) Utile pour le débogage et le test