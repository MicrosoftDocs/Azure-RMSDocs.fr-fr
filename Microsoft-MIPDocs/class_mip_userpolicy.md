# <a name="class-mipuserpolicy"></a>mip::UserPolicy, classe 
Représente la stratégie associée au contenu protégé.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public bool AccessCheck | Vérifie si la stratégie accorde à l’utilisateur l’accès au droit spécifié.
public UserPolicyType GetType | Obtient le type de stratégie.
public std::string GetName | Obtient le nom de la stratégie.
public std::string GetDescription | Obtient la description de la stratégie.
public std::shared_ptr< TemplateDescriptor > GetTemplateDescriptor public std::shared_ptr< PolicyDescriptor > GetPolicyDescriptor public std::string GetOwner | Obtient l’adresse e-mail du propriétaire du contenu.
public std::string GetIssuedTo | Obtient l’utilisateur associé à la stratégie de protection.
public bool IsIssuedToOwner | Obtient une valeur qui détermine si l’utilisateur actuel est le propriétaire du contenu.
public std::string GetContentId | Obtient l’identificateur unique du document/contenu.
public const mip::AppDataHashMap GetEncryptedAppData | Obtient les données spécifiques de l’application qui ont été chiffrées.
public const mip::AppDataHashMap GetSignedAppData | Obtient les données spécifiques de l’application qui ont été signées.
public std::chrono::time_point< std::chrono::system_clock > GetContentValidUntil | Obtient l’heure d’expiration de la stratégie.
public bool DoesUseDeprecatedAlgorithms | Obtient une valeur qui détermine si la stratégie utilise des algorithmes de chiffrement dépréciés pour la compatibilité descendante.
public bool IsAuditedExtractAllowed | Obtient une valeur qui détermine si la stratégie accorde le droit « audited extract » à l’utilisateur.
public const std::vector< unsigned char > GetSerializedPolicy public std::shared_ptr< rmscore::core::ProtectionPolicy > GetImpl
## <a name="members"></a>Membres
### <a name="accesscheck"></a>AccessCheck
Vérifie si la stratégie accorde à l’utilisateur l’accès au droit spécifié.
#### <a name="parameters"></a>Paramètres
* right : droit à vérifier
#### <a name="returns"></a>Returns
Une valeur indiquant si la stratégie accorde à l’utilisateur l’accès au droit spécifié
### <a name="userpolicytype"></a>UserPolicyType
Obtient le type de stratégie.
#### <a name="returns"></a>Returns
Type de stratégie
### <a name="getname"></a>GetName
Obtient le nom de la stratégie.
#### <a name="returns"></a>Returns
Nom de la stratégie
### <a name="getdescription"></a>GetDescription
Obtient la description de la stratégie.
#### <a name="returns"></a>Returns
Description de la stratégie
### <a name="templatedescriptor"></a>TemplateDescriptor
Obtient le [TemplateDescriptor](#classmip_1_1_template_descriptor) pour une [UserPolicy](#classmip_1_1_user_policy) basée sur des modèles.
#### <a name="returns"></a>Returns
[TemplateDescriptor](#classmip_1_1_template_descriptor) si [UserPolicy](#classmip_1_1_user_policy) est basé sur des modèles ; sinon, nullptr
### <a name="policydescriptor"></a>PolicyDescriptor
Obtient le [PolicyDescriptor](#classmip_1_1_policy_descriptor) pour une [UserPolicy](#classmip_1_1_user_policy) ad hoc.
#### <a name="returns"></a>Returns
[PolicyDescriptor](#classmip_1_1_policy_descriptor) si [UserPolicy](#classmip_1_1_user_policy) est ad hoc ; sinon, nullptr
### <a name="getowner"></a>GetOwner
Obtient l’adresse e-mail du propriétaire du contenu.
#### <a name="returns"></a>Returns
Adresse e-mail du propriétaire du contenu
### <a name="getissuedto"></a>GetIssuedTo
Obtient l’utilisateur associé à la stratégie de protection.
#### <a name="returns"></a>Returns
Utilisateur associé à la stratégie de protection
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Obtient une valeur qui détermine si l’utilisateur actuel est le propriétaire du contenu.
#### <a name="returns"></a>Returns
Valeur qui détermine si l’utilisateur actuel est le propriétaire du contenu
### <a name="getcontentid"></a>GetContentId
Obtient l’identificateur unique du document/contenu.
#### <a name="returns"></a>Returns
Identificateur unique du contenu
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtient les données spécifiques de l’application qui ont été chiffrées.
Une [UserPolicy](#classmip_1_1_user_policy) peut contenir un dictionnaire des données spécifiques de l’application qui ont été chiffrées par le service RMS. Ces données chiffrées ne dépendent pas des données signées accessibles par [UserPolicy::GetSignedAppData](#classmip_1_1_user_policy_1a1c8a284d50adcac1a0a09316afa1d43e)
### <a name="mipappdatahashmap"></a>mip::AppDataHashMap
Obtient les données spécifiques de l’application qui ont été signées.
Une [UserPolicy](#classmip_1_1_user_policy) peut contenir un dictionnaire des données spécifiques de l’application qui ont été signées par le service RMS. Ces données signées ne dépendent pas des données chiffrées accessibles par [UserPolicy::GetEncryptedAppData](#classmip_1_1_user_policy_1a610fbc799284ab0ce4354c0611ece0e8)
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtient l’heure d’expiration de la stratégie.
#### <a name="returns"></a>Returns
Heure d’expiration de la stratégie
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Obtient une valeur qui détermine si la stratégie utilise des algorithmes de chiffrement dépréciés pour la compatibilité descendante.
#### <a name="returns"></a>Returns
Valeur qui détermine si la stratégie utilise des algorithmes de chiffrement dépréciés
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Obtient une valeur qui détermine si la stratégie accorde le droit « audited extract » à l’utilisateur.
#### <a name="returns"></a>Returns
Valeur qui détermine si la stratégie accorde le droit « audited extract » à l’utilisateur
### <a name="getserializedpolicy"></a>GetSerializedPolicy
Sérialiser [UserPolicy](#classmip_1_1_user_policy) dans une licence de publication
#### <a name="returns"></a>Returns
[UserPolicy](#classmip_1_1_user_policy) sérialisée
### <a name="getimpl"></a>GetImpl
Obtient l’implémentation de la classe dérivée interne de [UserPolicy](#classmip_1_1_user_policy).
#### <a name="returns"></a>Returns
Implémentation de la classe dérivée de [UserPolicy](#classmip_1_1_user_policy) (interne uniquement)