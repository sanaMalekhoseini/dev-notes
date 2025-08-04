Swagger (l5-swagger)

نصب:

composer require "darkaonline/l5-swagger"
php artisan vendor:publish --provider "L5Swagger\L5SwaggerServiceProvider"

ساخت داکیومنت:
/**
* @param RegisterRequest $request
* @return JsonResponse
*
* @OA\Post(
*     path="/api/register",
*     summary="Register a new user",
*     tags={"auth"},
*     @OA\RequestBody(
*         required=true,
*         @OA\JsonContent(
*             @OA\Property (property="name", type="string",example="sana"),
*          @OA\Property (property="email",type="string", example="sana@gmail.com"),
*          @OA\Property (property="password",type="string", example="123456"),
*          @OA\Property (property="password_confrimation",type="string", example="123456"),
*
*         ),
*     ),
*     @OA\Response(
*         response=200,
*          description="user registerd successfuly",
*          @OA\JsonContent(
*              @OA\Property (property="token",type="string", description="Access token for user "),
*              @OA\Property (property="user", type="string", description="user details"),
*          ),
*     ),@OA\Response(
*          response=422,
*           description="validation error",
*           @OA\JsonContent (
*               @OA\Property (property="message",type="string", description="request not valid "),
*           ),
*      ),
* ),
*
* @OA\Info(
*       version="0.0.0",
*       title="Anophel API Documentation"
*   )
*/
php artisan l5-swagger:generate

نکات مهم:

@OA\Info باید حتما در یکی از فایل‌های controller بالا باشه

خطای @OA\Info not found یعنی تعریف اولیه انجام نشده

⏳ مرور هفتگی

✅ هفته اول:
- Gitflow
- اجرای artisan در Docker
- Swagger setup در Laravel