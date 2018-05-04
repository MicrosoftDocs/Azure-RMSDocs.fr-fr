# <a name="class-mipgetuserpolicyresult"></a>mip::GetUserPolicyResult, classe 
Décrit les résultats d’une demande d’acquisition de stratégie utilisateur.
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public GetUserPolicyResultStatus GetResultStatus | Obtient l’état de la demande d’acquisition de stratégie.
public std::shared_ptr< std::string > GetReferrer | Obtient l’adresse du référent de la stratégie.
public std::shared_ptr< UserPolicy > GetPolicy
## <a name="members"></a>Membres
### <a name="getuserpolicyresultstatus"></a>GetUserPolicyResultStatus
Obtient l’état de la demande d’acquisition de stratégie.
#### <a name="returns"></a>Returns
État de la demande d’acquisition de stratégie
### <a name="getreferrer"></a>GetReferrer
Obtient l’adresse du référent de la stratégie.
#### <a name="returns"></a>Returns
Adresse du référent de la stratégie. Le référent est un URI qui peut être affiché à l’utilisateur en cas d’échec de l’acquisition de la stratégie. L’URI contient des informations indiquant de quelle façon cet utilisateur peut obtenir l’autorisation d’accéder au contenu.
### <a name="userpolicy"></a>UserPolicy
Obtient une instance [UserPolicy](#classmip_1_1_user_policy).
#### <a name="returns"></a>Returns
lnstance [UserPolicy](#classmip_1_1_user_policy) si l’acquisition a réussi ; sinon, nullptr