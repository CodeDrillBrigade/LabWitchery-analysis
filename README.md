# Lab Witchery

## Scope

- Un applicazione per registrare materiali, gestire inserimento e consumo.
- Divisione dei materiali per luogo.
- A ogni materiale puo' essere assegnato tag.
- Funzionalita' di ricerca:
  - Nome (fuzzy)
  - Tipo materiali
- Alert sotto una certa soglia
  - Notifca nel programma
  - Mail
  - Telegram (secondario)
- Alert per scadenza
- Summary alert giornaliero / settimanale

## Data Model

### Box

```
{
	id: UUID;
	materialName: String;
  quantity: Int;
  metric: ENUM;
  subUnit: {
    quantity: Int;
    subUnit: { value: Float; metric: ENUM }?
  }?
  note: String?;
  status: ENUM;
  position: UUID;
  expirationDate: Date?;
}
```

### Material

```
{
  name: String;
  boxDefinition: {
    quantity: Int;
    metric: ENUM;
    subUnit: {
      quantity: Int;
      subUnit: { value: Float; metric: ENUM }?
    }?
  };
  brand: String;
	tags: Set<Tag>;
	description: String;
	noteList: List<{user: User, date: Date, message: String}>
}
```

### UsageLog

```
{
	date: Date,
	user: UUID;
	box: UUID;
	operation: ENUM;
	quantity: {
    quantity: Int;
    metric: ENUM;
    subUnit: {
      quantity: Int;
      subUnit: { value: Float; metric: ENUM }?
    }?
  };
}
```

### Storage

```
{
	ID: UUID;
	room: String;
	cabinet: String;
	shelf: String;
	closet: String?;
	box: String?;
}
```

### User

```
{
	ID: UUID;
	username: String;
	password: Hash&Salt;
	roles: Set<Role>;
	name: String;
	surname: String;
	contacts: Contacts[];
}
```

## Technologies

### Application Server

Kotlin + Spring

### Database

MongoDB

### Frontend

React
