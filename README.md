## Steps to Run the App

1. Run:
flutter pub get
2. Run:
flutter packages pub run build_runner build --delete-conflicting-outputs
3. Start the app on an emulator or device:
flutter run


## Code Choices:
 Architecture:
Clean Architecture
- the App’s main feature is in \lib\features\monitoring, this path contains the clean architecture layers.
- Dependency injection is implemented across the app using injectable and get_it.

 API Calls & Data Handling: Implemented using Dio
- MonitoringDatasource class monitoring_datasource.dart is responsible for interacting with the external
API, for http requests, I used the Dio package which is also used for caching
- BaseApiRepository class base_api_repository.dart:
This base class wraps all the API calls that come from the service MonitoringDatasource and returns a
DataState.
This class also hold the Error handling.
- DataState class data_state.dart:
This structure allows easy handling of success and failure states when making network requests.
- MonitoringRequestParams class monitoring_request_params.dart:
to wrap the parameters of the API request.
- MonitoringDataModel class monitoring_data_model.dart:
a model for the data that is returned.

 State Management: Used Flutter Bloc (Cubit).
The state class MonitoringState monitoring_state.dart, is annotated with freezed, for immutable states and
less boiler code.
 Caching: Implemented using Dio Cache Interceptor.

 Routing:
Implemented using auto_route and auto_route_generator packages, the package is also used for tab
switching.

 UI:
- navigation_bar_page.dart is the initial route, contains the navigation bar page that forms the apps home
page.
- monitoring_page_content.dart is the widget that is used across the three tabs
(battery_consumption_page.dart, house_consumption_page.dart, solar_generation_page.dart).
it contains the filters, the line charts, and the pull to refresh functionality.
for parameters it takes cubit, title, and fetchFunction which is the function the fetches data.
- line_chart_widget.dart is the LineChart Widget.
