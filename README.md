<p align="center"><a href="https://datatables.net/examples/styling/bootstrap4"><img src="https://drive.google.com/uc?export=view&id=1BixUms5LUlR6-6TE3tPASyuTE1QtKLC_"></a></p>

# Vue Datatables

> Server Side Processing Datatables written with Vuejs Framework.

Reference: https://datatables.net/examples/styling/bootstrap4

## The Problem

> Rendering a table of over 5k records on the client-side will make the browser crush.

## The Solution

> By leveraging of server-side pagination we gain a preformance advantange.

## Usage

Choose whatever component you need:
```html
<div id="app">
    <datatable-wrapper>
        <datatable-header>
            <datatable-perpage :perPage="perPage" 
                               @perPageChanged="onPerPageChanged">
            </datatable-perpage>
            <datatable-search @searching="onSearch"></datatable-search>
        </datatable-header>
        <datatable url="http://localhost:3000/people" 
                   :data="requestData"
                   @gettingRecords="onGettingRecords"
                   @recordsFetched="onRecordsFetched">
                <datatable-loader :loading="loading"></datatable-loader>
                <datatable-head :columns="columns" 
                                @columnClicked="onColumnClicked">
                </datatable-head>
                <datatable-body :columns="columns" 
                                :records="records">
                </datatable-body>
                <datatable-footer :columns="columns"></datatable-footer>
        </datatable>
        <datatable-pagination :short="pagination.totalPages > 10 ? true : false"
                              :pagination="pagination"
                              @prev="requestData.page = arguments[0]"
                              @next="requestData.page = arguments[0]"
                              @linkClicked="requestData.page = arguments[0]">
        </datatable-pagination>
    </datatable-wrapper>
</div>
```

## Components Events

| Component                 | Events                         |
| ------------------------- | ------------------------------ |
| `<datatable-perpage/>`    | perPageChanged                 |
| `<datatable-search/>`     | searching                      |
| `<datatable/>`            | gettingRecords, recordsFetched |
| `<datatable-loader/>`     | loading                        |
| `<datatable-head/>`       | columnClicked                  |
| `<datatable-pagination/>` | prev, next, linkClicked        |


## Server-Side

> In general the datatable will make an ajax request to the given url and expects a JSON response in the following format:
```javascript
{
  "columns": [
    {
      "name": "id",
      "label": "#",
      "width": "33%"
    },
    {
      "name": "email",
      "label": "Email",
      "width": "33%"
    },
    {
      "name": "phone",
      "label": "Phone",
      "width": "33%"
    }
  ],
  "data": [
    {
      "id": 1,
      "email": "Willow_Kassulke91@gmail.com",
      "phone": "1-196-138-6202 x30775"
    },
    ...
  ],
  "pagination": {
    "currentPage": 1,
    "nextPage": 2,
    "prevPage": 1,
    "lastPage": 50,
    "total": 50,
    "totalPages": 5,
    "lastPageUrl": "?page=5", // optional
    "nextPageUrl": "?page=2", // optional
    "prevPageUrl": "?page=1", // optional
    "from": 1,
    "to": 10
  }
}
```

This example will create a table with 3 columns: id, name, email.
Usable classes for generating this kind of response on the server-side comming up soon.

## Build

Seed dummy data
```sh
./datatables seed --records 150
```

Run demo server
```sh
npm run demo-server
```

## Todo

- [ ] Set config file where the user can put his database configurations.
- [x] Allow the users to hide columns.
- [ ] Add action component to allow editing or creation of new records. 