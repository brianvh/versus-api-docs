# URL Path Parameters

Due to the REST nature of the Versus API endpoints, extensive use of URL Path Parameters is made. Since several endpoints use multiple URL Path parameters, and the entire set is realtively small, this section will describe all URL Path parameters in use.

Parameter | Description
--------- | -----------
:game_uuid | Versus ID of the Game. This is required in every endpoint path.
:player_uuid | Versus ID of a player associated with the Publisher of the Game. Sometimes used as a normal parameter.
:tournament_uuid | Versus ID for a Tournament, owned by the Game.
:slot_uuid | Versus ID for a Player Slot, owned by a Tournament.
:purchase_uuid | Versus ID for a credit bundle Purchase.
:payout_uuid | Versus ID for a credit Payout request.

<aside class="warning">If a URL endpoint specifies one or more of these parameters, they must be provided. If an incorrect value is supplied, a 404 error will be returned.</aside>