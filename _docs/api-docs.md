---
layout: default
title: API 문서
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DevPals API Docs</title>
    <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/4.15.5/swagger-ui.css" />
    <style>
        html {
            box-sizing: border-box;
            overflow: -moz-scrollbars-vertical;
            overflow-y: scroll;
        }
        * {
            box-sizing: inherit;
        }
        body {
            margin: 0;
            background: #fafafa;
        }
    </style>
</head>
<body>
    <div id="swagger-ui"></div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/4.15.5/swagger-ui-bundle.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/4.15.5/swagger-ui-standalone-preset.js"></script>
    <script>
        window.onload = function() {
            const spec = {
  "openapi": "3.0.0",
  "paths": {
    "/": {
      "get": {
        "operationId": "AppController_getHello",
        "parameters": [],
        "responses": {
          "200": {
            "description": ""
          }
        },
        "tags": [
          "App"
        ]
      }
    },
    "/auth/sign-up": {
      "post": {
        "description": "사용자의 이메일, 닉네임, 비밀번호를 통해 회원가입을 처리합니다.",
        "operationId": "AuthController_postSignUp",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/SignUpDto"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "회원 가입 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "success": true,
                    "message": "회원가입이 완료되었습니다.",
                    "user": {
                      "id": 1,
                      "email": "devpals@mail.com",
                      "nickname": "김개발"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "유효성 검사 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 400,
                    "message": [
                      "이메일을 입력해주세요.",
                      "비밀번호는 8자 이상 20자 이하로 입력해주세요."
                    ],
                    "error": "Bad Request"
                  }
                }
              }
            }
          }
        },
        "summary": "회원가입",
        "tags": [
          "auth"
        ]
      }
    },
    "/auth/login": {
      "post": {
        "description": "이메일과 비밀번호로 로그인하여 JWT를 반환합니다.",
        "operationId": "AuthController_postLogin",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/LoginDto"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "로그인 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "success": true,
                    "message": "로그인 되었습니다.",
                    "data": {
                      "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
                      "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
                    },
                    "user": {
                      "id": 8,
                      "email": "devpals@mail.com",
                      "nickname": "김개발"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "가입되지 않은 계정",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "success": false,
                    "message": "가입되지 않은 계정입니다.",
                    "data": null
                  }
                }
              }
            }
          },
          "401": {
            "description": "인증에 실패했습니다."
          }
        },
        "summary": "로그인",
        "tags": [
          "auth"
        ]
      }
    },
    "/auth/password/reset": {
      "post": {
        "description": "이메일과 인증 코드를 통해 비밀번호를 재설정합니다.",
        "operationId": "AuthController_postResetPassword",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/ResetPasswordDto"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "비밀번호가 성공적으로 재설정되었습니다.",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "success": true,
                    "message": "비밀번호가 성공적으로 재설정되었습니다."
                  }
                }
              }
            }
          }
        },
        "summary": "비밀번호 재설정",
        "tags": [
          "auth"
        ]
      }
    },
    "/auth/logout": {
      "post": {
        "description": "로그아웃을 수행하고 세션을 무효화합니다.",
        "operationId": "AuthController_postLogout",
        "parameters": [],
        "responses": {
          "201": {
            "description": "로그아웃 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "로그아웃에 성공했습니다"
                  }
                }
              }
            }
          },
          "401": {
            "description": "JWT 인증 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 401,
                    "message": "유효하지 않거나 만료된 토큰입니다",
                    "error": "Unauthorized"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "로그아웃",
        "tags": [
          "auth"
        ]
      }
    },
    "/auth/refresh": {
      "post": {
        "description": "리프레시 토큰을 사용해 새로운 액세스 토큰과 리프레시 토큰을 발급받습니다.",
        "operationId": "AuthController_postRefresh",
        "parameters": [],
        "requestBody": {
          "required": true,
          "description": "리프레시 토큰 요청 본문",
          "content": {
            "application/json": {
              "schema": {
                "example": {
                  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "새로운 액세스 및 리프레시 토큰 발급 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "success": true,
                    "message": "토큰 갱신 성공",
                    "data": {
                      "accessToken": "new_access_token",
                      "refreshToken": "new_refresh_token"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "유효하지 않거나 만료된 리프레시 토큰",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "success": false,
                    "message": "Invalid refresh token"
                  }
                }
              }
            }
          }
        },
        "summary": "토큰 갱신",
        "tags": [
          "auth"
        ]
      }
    },
    "/authenticode/send": {
      "post": {
        "description": "입력된 이메일로 인증 코드를 발송합니다.",
        "operationId": "AuthenticodeController_postSendEmailCode",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/SendEmailCodeDto"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "인증 코드가 이메일로 전송되었습니다."
          },
          "400": {
            "description": "유효한 이메일을 입력해주세요."
          },
          "500": {
            "description": "서버 내부 오류로 인해 메일 발송에 실패했습니다."
          }
        },
        "summary": "이메일 인증 코드 발송",
        "tags": [
          "authenticode"
        ]
      }
    },
    "/authenticode/verify": {
      "post": {
        "description": "사용자가 입력한 이메일과 인증 코드의 유효성을 확인합니다.",
        "operationId": "AuthenticodeController_postVerifyEmailCode",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/VerifyEmailCodeDto"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "인증 코드가 확인되었습니다."
          },
          "400": {
            "description": "유효한 이메일을 입력해주세요."
          },
          "401": {
            "description": "인증 코드가 만료되었습니다."
          },
          "500": {
            "description": "서버 내부 오류로 인해 인증 코드 확인에 실패했습니다."
          }
        },
        "summary": "이메일 인증 코드 확인",
        "tags": [
          "authenticode"
        ]
      }
    },
    "/project/{id}/applicant": {
      "post": {
        "description": "지원자가 공고를 지원합니다.",
        "operationId": "ApplicantController_postApplicant",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/CreateApplicantDTO"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "공고 지원하기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "id": 9,
                    "userId": 8,
                    "projectId": 68,
                    "message": "기획자에게 하고 싶은 말",
                    "email": "devpals@mail.com",
                    "phoneNumber": "010-0000-0000",
                    "career": [
                      {
                        "name": "string",
                        "periodStart": "2025-01-10",
                        "periodEnd": "2025-01-10",
                        "role": "string"
                      }
                    ],
                    "status": "WAITING",
                    "createdAt": "2025-01-09T00:34:03.000Z",
                    "updatedAt": "2025-01-09T00:34:03.000Z"
                  }
                }
              }
            }
          },
          "400": {
            "description": "0 또는 숫자로 입력하지 않았을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "Invalid ID: ID must be a valid number and not 0.",
                    "error": "Bad Request",
                    "statusCode": 400
                  }
                }
              }
            }
          },
          "403": {
            "description": "본인이 등록한 공고에 지원할 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "본인이 등록한 공고에 지원할 수 없습니다.",
                    "error": "Forbidden",
                    "statusCode": 403
                  }
                }
              }
            }
          },
          "404": {
            "description": "공고가 존재하지 않을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고는 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          },
          "409": {
            "description": "이미 지원한 공고에 지원할 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "이미 지원한 공고입니다.",
                    "error": "Conflict",
                    "statusCode": 409
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "공고 지원하기",
        "tags": [
          "applicant"
        ]
      },
      "get": {
        "description": "관리자(본인)가 지원자 목록을 확인합니다.",
        "operationId": "ApplicantController_getManyApplicant",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "공고 지원자 목록 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": [
                    {
                      "id": 7,
                      "userId": 8,
                      "projectId": 6,
                      "message": "기획자에게 하고 싶은 말",
                      "email": "devpals@mail.com",
                      "phoneNumber": "010-9999-0000",
                      "career": null,
                      "status": "REJECTED",
                      "createdAt": "2025-01-08T17:54:43.000Z",
                      "updatedAt": "2025-01-09T09:01:59.000Z",
                      "User": {
                        "id": 8,
                        "nickname": "김개발"
                      }
                    }
                  ]
                }
              }
            }
          },
          "403": {
            "description": "해당 공고 작성자(기획자)가 아닌 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고의 기획자만 조회 가능합니다.",
                    "error": "Forbidden",
                    "statusCode": 403
                  }
                }
              }
            }
          },
          "404": {
            "description": "해당 공고가 없는 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고는 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "공고 지원자 목록",
        "tags": [
          "applicant"
        ]
      }
    },
    "/project/{id}/applicant/summary": {
      "get": {
        "description": "관리자(본인)가 합격자/불합격자 목록을 확인합니다.",
        "operationId": "ApplicantController_getApplicantByStatus",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "공고 합격자/불합격자 목록 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "accepted": [
                      {
                        "id": 7,
                        "userId": 8,
                        "projectId": 6,
                        "message": "기획자에게 하고 싶은 말",
                        "email": "devpals@mail.com",
                        "phoneNumber": "010-0000-0000",
                        "career": null,
                        "status": "ACCEPTED",
                        "createdAt": "2025-01-08T17:54:43.000Z",
                        "updatedAt": "2025-01-09T10:07:20.000Z",
                        "User": {
                          "id": 8,
                          "nickname": "김개발",
                          "email": "devpals@mail.com",
                          "bio": null,
                          "profileImg": "프로필 이미지 주소",
                          "UserSkillTag": [
                            {
                              "userId": 8,
                              "skillTagId": 28,
                              "createdAt": "2025-01-08T11:57:17.000Z",
                              "SkillTag": {
                                "id": 28,
                                "name": "Figma",
                                "img": "스킬 태그 이미지 주소",
                                "createdAt": "2025-01-02T15:11:15.000Z"
                              }
                            }
                          ]
                        }
                      }
                    ],
                    "rejected": []
                  }
                }
              }
            }
          },
          "403": {
            "description": "해당 공고 작성자(기획자)가 아닌 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고의 기획자만 조회 가능합니다.",
                    "error": "Forbidden",
                    "statusCode": 403
                  }
                }
              }
            }
          },
          "404": {
            "description": "해당 공고가 없는 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고는 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "공고 합격자/불합격자 목록",
        "tags": [
          "applicant"
        ]
      }
    },
    "/project/{id}/applicant/{applicantUserId}/status": {
      "patch": {
        "description": "관리자(본인)가 지원자의 상태를 변경합니다.",
        "operationId": "ApplicantController_patchApplicantByStatus",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "applicantUserId",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/ModifyApplicantStatusDTO"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "지원자의 상태 변경 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "id": 7,
                    "userId": 8,
                    "projectId": 6,
                    "message": "기획자에게 하고 싶은 말",
                    "email": "devpals@mail.com",
                    "phoneNumber": null,
                    "career": null,
                    "status": "REJECTED",
                    "createdAt": "2025-01-08T17:54:43.000Z",
                    "updatedAt": "2025-01-09T10:48:35.000Z"
                  }
                }
              }
            }
          },
          "400": {
            "description": "같은 상태로 바꾸려고 하는 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "상태가 이미 동일합니다.",
                    "error": "Bad Request",
                    "statusCode": 400
                  }
                }
              }
            }
          },
          "403": {
            "description": "해당 공고 작성자(기획자)가 아닌 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "기획자만 수정 가능합니다.",
                    "error": "Forbidden",
                    "statusCode": 403
                  }
                }
              }
            }
          },
          "404": {
            "description": "해당 공고가 없는 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고는 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "지원자 상태 변경",
        "tags": [
          "applicant"
        ]
      }
    },
    "/project/{id}/applicant/{applicantUserId}": {
      "get": {
        "description": "관리자(본인)가 지원자 정보를 확인합니다.",
        "operationId": "ApplicantController_getApplicant",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "applicantUserId",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "공고 지원자 정보 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "id": 7,
                    "userId": 8,
                    "projectId": 6,
                    "message": "하고싶은말",
                    "email": "",
                    "phoneNumber": "010-1111-1111",
                    "career": [
                      {
                        "name": "string",
                        "role": "string",
                        "periodEnd": "string",
                        "periodStart": "string"
                      }
                    ],
                    "status": "REJECTED",
                    "createdAt": "2025-01-08T17:54:43.000Z",
                    "updatedAt": "2025-01-10T09:29:06.000Z",
                    "User": {
                      "id": 8,
                      "nickname": "김개발데브",
                      "email": "devpals@mail.com",
                      "bio": "새로운 소개글입니다.",
                      "profileImg": "프로필이미지",
                      "UserSkillTag": [
                        {
                          "userId": 8,
                          "skillTagId": 1,
                          "createdAt": "2025-01-13T09:26:01.000Z",
                          "SkillTag": {
                            "id": 1,
                            "name": "JavaScript",
                            "img": "스킬태그이미지",
                            "createdAt": "2025-01-02T15:07:03.000Z"
                          }
                        }
                      ]
                    }
                  }
                }
              }
            }
          },
          "403": {
            "description": "해당 공고 작성자(기획자)가 아닌 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고의 기획자만 조회 가능합니다.",
                    "error": "Forbidden",
                    "statusCode": 403
                  }
                }
              }
            }
          },
          "404": {
            "description": "해당 공고가 없는 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고는 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "공고 지원자 상세보기",
        "tags": [
          "applicant"
        ]
      }
    },
    "/position-tag": {
      "get": {
        "description": "포지션 태그 목록을 가져옵니다.",
        "operationId": "PositionTagController_getManyPositionTag",
        "parameters": [],
        "responses": {
          "200": {
            "description": "포지션 태그 목록 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": [
                    {
                      "id": 1,
                      "name": "백엔드",
                      "createdAt": "2025-01-02T12:19:48.000Z"
                    },
                    {
                      "id": 2,
                      "name": "프론트엔드",
                      "createdAt": "2025-01-02T12:19:51.000Z"
                    },
                    {
                      "id": 3,
                      "name": "디자이너",
                      "createdAt": "2025-01-02T12:19:55.000Z"
                    },
                    {}
                  ]
                }
              }
            }
          }
        },
        "summary": "포지션 태그 목록",
        "tags": [
          "position-tag"
        ]
      }
    },
    "/skill-tag": {
      "get": {
        "description": "스킬 태그 목록을 가져옵니다.",
        "operationId": "SkillTagController_getManySkillTag",
        "parameters": [],
        "responses": {
          "200": {
            "description": "스킬 태그 목록 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": [
                    {
                      "id": 1,
                      "name": "JavaScript",
                      "img": "스킬 태그 이미지 주소",
                      "createdAt": "2025-01-02T15:07:03.000Z"
                    },
                    {
                      "id": 2,
                      "name": "TypeScript",
                      "img": "스킬 태그 이미지 주소",
                      "createdAt": "2025-01-02T15:07:23.000Z"
                    },
                    {
                      "id": 3,
                      "name": "React",
                      "img": "스킬 태그 이미지 주소",
                      "createdAt": "2025-01-02T15:07:31.000Z"
                    },
                    {}
                  ]
                }
              }
            }
          }
        },
        "summary": "스킬 태그 목록",
        "tags": [
          "skill-tag"
        ]
      }
    },
    "/project": {
      "get": {
        "description": "등록순으로 공고 목록을 보여줍니다.",
        "operationId": "ProjectController_getManyProject",
        "parameters": [
          {
            "name": "skillTag",
            "required": false,
            "in": "query",
            "description": "스킬 태그",
            "schema": {
              "example": [
                1,
                2
              ],
              "type": "array",
              "items": {
                "type": "number"
              }
            }
          },
          {
            "name": "positionTag",
            "required": false,
            "in": "query",
            "description": "포지션 태그",
            "schema": {
              "example": 1,
              "type": "number"
            }
          },
          {
            "name": "methodId",
            "required": false,
            "in": "query",
            "description": "진행 방식",
            "schema": {
              "example": 1,
              "type": "number"
            }
          },
          {
            "name": "isBeginner",
            "required": false,
            "in": "query",
            "description": "새싹 가능",
            "schema": {
              "example": true,
              "type": "boolean"
            }
          },
          {
            "name": "keyword",
            "required": false,
            "in": "query",
            "description": "공고 제목 또는 설명 검색",
            "schema": {
              "example": "공고 제목, 설명",
              "type": "string"
            }
          },
          {
            "name": "page",
            "required": true,
            "in": "query",
            "description": "페이지 번호",
            "schema": {
              "example": 1,
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "공고 목록 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "projects": [
                      {
                        "id": 68,
                        "title": "클론코딩 사이드 프로젝트 모집 공고",
                        "description": "string",
                        "totalMember": 3,
                        "startDate": "2025-01-25T00:00:00.000Z",
                        "estimatedPeriod": "3개월",
                        "methodId": 1,
                        "authorId": 8,
                        "views": 2,
                        "isBeginner": true,
                        "isDone": true,
                        "recruitmentEndDate": "2025-02-15T00:00:00.000Z",
                        "recruitmentStartDate": "2025-01-06T00:00:00.000Z",
                        "createdAt": "2025-01-06T21:19:21.000Z",
                        "updatedAt": "2025-01-06T21:19:21.000Z",
                        "User": {
                          "id": 8,
                          "nickname": "김개발",
                          "email": "devpals@mail.com",
                          "bio": null,
                          "profileImg": "프로필 이미지 주소",
                          "createdAt": "2025-01-04T06:39:31.000Z",
                          "updatedAt": "2025-01-08T18:15:13.000Z"
                        },
                        "ProjectSkillTag": [
                          {
                            "projectId": 68,
                            "skillTagId": 12,
                            "SkillTag": {
                              "id": 12,
                              "name": "Kotlin",
                              "img": "스킬 태그 이미지 주소",
                              "createdAt": "2025-01-02T15:09:19.000Z"
                            }
                          }
                        ],
                        "Method": {
                          "id": 1,
                          "name": "온라인",
                          "createdAt": "2025-01-02T12:36:01.000Z"
                        },
                        "ProjectPositionTag": [
                          {
                            "projectId": 68,
                            "positionTagId": 1,
                            "PositionTag": {
                              "id": 1,
                              "name": "백엔드",
                              "createdAt": "2025-01-02T12:19:48.000Z"
                            }
                          },
                          {
                            "projectId": 68,
                            "positionTagId": 2,
                            "PositionTag": {
                              "id": 2,
                              "name": "프론트엔드",
                              "createdAt": "2025-01-02T12:19:51.000Z"
                            }
                          }
                        ]
                      },
                      {}
                    ],
                    "total": 67,
                    "currentPage": 1,
                    "lastPage": 6
                  }
                }
              }
            }
          }
        },
        "summary": "공고 목록",
        "tags": [
          "project"
        ]
      },
      "post": {
        "description": "공고를 생성합니다.",
        "operationId": "ProjectController_postProject",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/CreateProjectDTO"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "공고 등록 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "id": 10,
                    "title": "클론코딩 사이드 프로젝트 모집 공고",
                    "description": "string",
                    "totalMember": 3,
                    "startDate": "2025-01-25T00:00:00.000Z",
                    "estimatedPeriod": "3개월",
                    "methodId": 1,
                    "authorId": 8,
                    "views": 0,
                    "isBeginner": true,
                    "isDone": false,
                    "recruitmentEndDate": "2025-02-15T00:00:00.000Z",
                    "recruitmentStartDate": "2025-01-06T00:00:00.000Z",
                    "createdAt": "2025-01-06T07:05:01.000Z",
                    "updatedAt": "2025-01-06T07:05:01.000Z"
                  }
                }
              }
            }
          },
          "404": {
            "description": "스킬 태그가 존재하지 않을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 스킬 태그 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "공고 등록하기",
        "tags": [
          "project"
        ]
      }
    },
    "/project/count": {
      "get": {
        "description": "진행중 / 마감 / 전체 공고 개수를 보여줍니다.",
        "operationId": "ProjectController_getProjectCount",
        "parameters": [],
        "responses": {
          "200": {
            "description": "공고 개수 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "ongoingProjectCount": 63,
                    "endProjectCount": 4,
                    "totalProjectCount": 67
                  }
                }
              }
            }
          }
        },
        "summary": "진행중 / 마감 / 전체 공고 개수",
        "tags": [
          "project"
        ]
      }
    },
    "/project/my": {
      "get": {
        "description": "기획자(본인)가 등록한 공고 목록을 등록순으로 보여줍니다.",
        "operationId": "ProjectController_getManyMyProject",
        "parameters": [],
        "responses": {
          "200": {
            "description": "공고 목록 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": [
                    {
                      "id": 68,
                      "title": "클론코딩 사이드 프로젝트 모집 공고",
                      "description": "string",
                      "totalMember": 3,
                      "startDate": "2025-01-25T00:00:00.000Z",
                      "estimatedPeriod": "3개월",
                      "methodId": 1,
                      "authorId": 8,
                      "views": 2,
                      "isBeginner": true,
                      "isDone": true,
                      "recruitmentEndDate": "2025-02-15T00:00:00.000Z",
                      "recruitmentStartDate": "2025-01-06T00:00:00.000Z",
                      "createdAt": "2025-01-06T21:19:21.000Z",
                      "updatedAt": "2025-01-06T21:19:21.000Z",
                      "ProjectSkillTag": [
                        {
                          "projectId": 68,
                          "skillTagId": 12,
                          "SkillTag": {
                            "id": 12,
                            "name": "Kotlin",
                            "img": "스킬 태그 이미지 주소",
                            "createdAt": "2025-01-02T15:09:19.000Z"
                          }
                        }
                      ],
                      "ProjectPositionTag": [
                        {
                          "projectId": 68,
                          "positionTagId": 1,
                          "PositionTag": {
                            "id": 1,
                            "name": "백엔드",
                            "createdAt": "2025-01-02T12:19:48.000Z"
                          }
                        },
                        {
                          "projectId": 68,
                          "positionTagId": 2,
                          "PositionTag": {
                            "id": 2,
                            "name": "프론트엔드",
                            "createdAt": "2025-01-02T12:19:51.000Z"
                          }
                        }
                      ]
                    },
                    {}
                  ]
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "기획자가 등록한 공고 목록",
        "tags": [
          "project"
        ]
      }
    },
    "/project/{id}": {
      "get": {
        "description": "공고를 상세히 보여줍니다.",
        "operationId": "ProjectController_getProject",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "공고 상세보기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "id": 10,
                    "title": "클론코딩 사이드 프로젝트 모집 공고",
                    "description": "string",
                    "totalMember": 3,
                    "startDate": "2025-01-25T00:00:00.000Z",
                    "estimatedPeriod": "3개월",
                    "methodId": 1,
                    "authorId": 8,
                    "views": 1,
                    "isBeginner": true,
                    "isDone": false,
                    "recruitmentEndDate": "2025-02-15T00:00:00.000Z",
                    "recruitmentStartDate": "2025-01-06T00:00:00.000Z",
                    "createdAt": "2025-01-06T07:05:01.000Z",
                    "updatedAt": "2025-01-06T07:05:01.000Z",
                    "User": {
                      "id": 8,
                      "nickname": "김개발",
                      "email": "devpals@mail.com",
                      "bio": null,
                      "profileImg": "프로필 이미지 주소",
                      "createdAt": "2025-01-04T06:39:31.000Z",
                      "updatedAt": "2025-01-08T18:15:13.000Z"
                    },
                    "ProjectSkillTag": [
                      {
                        "projectId": 10,
                        "skillTagId": 1,
                        "SkillTag": {
                          "id": 1,
                          "name": "JavaScript",
                          "img": "스킬 태그 이미지 주소",
                          "createdAt": "2025-01-02T15:07:03.000Z"
                        }
                      },
                      {
                        "projectId": 10,
                        "skillTagId": 2,
                        "SkillTag": {
                          "id": 2,
                          "name": "TypeScript",
                          "img": "스킬 태그 이미지 주소",
                          "createdAt": "2025-01-02T15:07:23.000Z"
                        }
                      }
                    ],
                    "Method": {
                      "id": 1,
                      "name": "온라인",
                      "createdAt": "2025-01-02T12:36:01.000Z"
                    },
                    "ProjectPositionTag": [
                      {
                        "projectId": 10,
                        "positionTagId": 1,
                        "PositionTag": {
                          "id": 1,
                          "name": "백엔드",
                          "createdAt": "2025-01-02T12:19:48.000Z"
                        }
                      },
                      {
                        "projectId": 10,
                        "positionTagId": 2,
                        "PositionTag": {
                          "id": 2,
                          "name": "프론트엔드",
                          "createdAt": "2025-01-02T12:19:51.000Z"
                        }
                      }
                    ],
                    "Applicant": []
                  }
                }
              }
            }
          },
          "400": {
            "description": "0 또는 숫자로 입력하지 않았을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "Invalid ID: ID must be a valid number and not 0.",
                    "error": "Bad Request",
                    "statusCode": 400
                  }
                }
              }
            }
          },
          "404": {
            "description": "공고가 존재하지 않을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 공고는 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          }
        },
        "summary": "공고 상세보기",
        "tags": [
          "project"
        ]
      },
      "put": {
        "description": "기획자(본인)가 공고를 수정합니다.",
        "operationId": "ProjectController_putProject",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/ModifyProjectDTO"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "공고 수정 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "id": 10,
                    "title": "클론코딩 사이드 프로젝트 모집 공고",
                    "description": "string",
                    "totalMember": 3,
                    "startDate": "2025-01-25T00:00:00.000Z",
                    "estimatedPeriod": "3개월",
                    "methodId": 1,
                    "authorId": 8,
                    "views": 0,
                    "isBeginner": true,
                    "isDone": false,
                    "recruitmentEndDate": "2025-02-15T00:00:00.000Z",
                    "recruitmentStartDate": "2025-01-06T00:00:00.000Z",
                    "createdAt": "2025-01-06T07:05:01.000Z",
                    "updatedAt": "2025-01-06T07:05:01.000Z"
                  }
                }
              }
            }
          },
          "403": {
            "description": "해당 공고 작성자(기획자)가 아닌 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "기획자만 수정 가능합니다.",
                    "error": "Forbidden",
                    "statusCode": 403
                  }
                }
              }
            }
          },
          "404": {
            "description": "스킬 태그가 존재하지 않을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "해당 스킬 태그 존재하지 않습니다.",
                    "error": "Not Found",
                    "statusCode": 404
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "공고 수정하기",
        "tags": [
          "project"
        ]
      }
    },
    "/project/{id}/is-done": {
      "patch": {
        "description": "기획자(본인)가 공고 모집을 종료합니다.",
        "operationId": "ProjectController_patchProjectIsDone",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "공고 모집 종료 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "id": 10,
                    "title": "클론코딩 사이드 프로젝트 모집 공고",
                    "description": "string",
                    "totalMember": 3,
                    "startDate": "2025-01-25T00:00:00.000Z",
                    "estimatedPeriod": "3개월",
                    "methodId": 1,
                    "authorId": 8,
                    "views": 0,
                    "isBeginner": true,
                    "isDone": true,
                    "recruitmentEndDate": "2025-02-15T00:00:00.000Z",
                    "recruitmentStartDate": "2025-01-06T00:00:00.000Z",
                    "createdAt": "2025-01-06T07:05:01.000Z",
                    "updatedAt": "2025-01-06T07:05:01.000Z"
                  }
                }
              }
            }
          },
          "403": {
            "description": "해당 공고 작성자(기획자)가 아닌 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "기획자만 모집을 종료할 수 있습니다.",
                    "error": "Forbidden",
                    "statusCode": 403
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "공고 모집 종료",
        "tags": [
          "project"
        ]
      }
    },
    "/method": {
      "get": {
        "description": "진행 방식 목록을 가져옵니다.",
        "operationId": "MethodController_getManyMethod",
        "parameters": [],
        "responses": {
          "200": {
            "description": "진행 방식 목록 가져오기 성공",
            "content": {
              "application/json": {
                "schema": {
                  "example": [
                    {
                      "id": 1,
                      "name": "온라인",
                      "createdAt": "2025-01-02T12:36:01.000Z"
                    },
                    {
                      "id": 2,
                      "name": "오프라인",
                      "createdAt": "2025-01-02T12:36:07.000Z"
                    },
                    {
                      "id": 3,
                      "name": "온/오프라인",
                      "createdAt": "2025-01-02T12:36:10.000Z"
                    }
                  ]
                }
              }
            }
          }
        },
        "summary": "진행 방식 목록",
        "tags": [
          "method"
        ]
      }
    },
    "/user/nickname-check": {
      "post": {
        "description": "입력된 닉네임이 이미 사용 중인지 확인합니다.",
        "operationId": "UserController_postNicknameCheck",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/CheckNicknameDto"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "닉네임 사용 가능",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "사용 가능한 닉네임입니다."
                  }
                }
              }
            }
          },
          "400": {
            "description": "잘못된 요청 (닉네임 형식 오류)",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": [
                      "닉네임은 반드시 입력해야 합니다."
                    ],
                    "error": "Bad Request",
                    "statusCode": 400
                  }
                }
              }
            }
          }
        },
        "summary": "닉네임 중복 확인",
        "tags": [
          "user"
        ]
      }
    },
    "/user/me/profile-img": {
      "patch": {
        "description": "사용자의 프로필 이미지를 파일 형식으로 업로드하고 업데이트합니다.",
        "operationId": "UserController_patchUpdateProfileImage",
        "parameters": [],
        "requestBody": {
          "required": true,
          "description": "업로드할 프로필 이미지 파일 (최대 5MB, png, jpg, jpeg)",
          "content": {
            "multipart/form-data": {
              "schema": {
                "type": "object",
                "properties": {
                  "file": {
                    "type": "string",
                    "format": "binary"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "프로필 이미지가 성공적으로 업데이트됨",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "프로필 이미지가 성공적으로 업데이트되었습니다.",
                    "user": {
                      "id": 1,
                      "nickname": "exampleUser",
                      "profileImg": "http://example.com/new-image.png"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "잘못된 요청 (파일이 첨부되지 않음)",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "message": "파일이 업로드되지 않았습니다.",
                    "error": "Bad Request",
                    "statusCode": 400
                  }
                }
              }
            }
          },
          "401": {
            "description": "인증 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 401,
                    "message": "유효하지 않거나 만료된 토큰입니다.",
                    "error": "Unauthorized"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "프로필 이미지 업데이트",
        "tags": [
          "user"
        ]
      }
    },
    "/user/me/applications": {
      "get": {
        "description": "사용자가 지원한 프로젝트 목록과 합격 여부를 반환합니다.<br>\n                  지원은 했으나 불합 처리 되지 않았어도, 모집 종료시 불합격입니다. 따라서 불/합 리스트만 보입니다.",
        "operationId": "UserController_getApplications",
        "parameters": [],
        "responses": {
          "200": {
            "description": "사용자의 지원한 프로젝트와 합격, 불합격에 따른 상태 반환",
            "content": {
              "application/json": {
                "schema": {
                  "example": [
                    {
                      "id": 1,
                      "projectTitle": "클론코딩 사이드 프로젝트 팀원 모집",
                      "status": "ACCEPTED"
                    },
                    {
                      "id": 2,
                      "projectTitle": "클론코딩 모집",
                      "status": "REJECTED"
                    }
                  ]
                }
              }
            }
          },
          "401": {
            "description": "인증 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 401,
                    "message": "유효하지 않거나 만료된 토큰입니다.",
                    "error": "Unauthorized"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "마이페이지 지원 정보 조회",
        "tags": [
          "user"
        ]
      }
    },
    "/user/me": {
      "get": {
        "description": "인증된 사용자의 정보를 반환하며, 포지션, 깃허브 링크, 경력, 스킬셋 등을 포함합니다.",
        "operationId": "UserController_getMyInfo",
        "parameters": [],
        "responses": {
          "200": {
            "description": "사용자의 정보 반환",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/MyInfoResponseDto"
                }
              }
            }
          },
          "401": {
            "description": "인증 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 401,
                    "message": "유효하지 않거나 만료된 토큰입니다.",
                    "error": "Unauthorized"
                  }
                }
              }
            }
          },
          "404": {
            "description": "사용자 정보가 존재하지 않을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 404,
                    "message": "사용자 정보를 찾을 수 없습니다.",
                    "error": "Not Found"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "내 정보 보기",
        "tags": [
          "user"
        ]
      },
      "put": {
        "description": "사용자의 정보를 수정합니다.",
        "operationId": "UserController_putUpdateMe",
        "parameters": [],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/UpdateUserDto"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "사용자 정보가 성공적으로 수정되었습니다.",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/MyInfoResponseDto"
                }
              }
            }
          },
          "400": {
            "description": "잘못된 요청 데이터 형식",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 400,
                    "message": "잘못된 데이터 형식입니다.",
                    "error": "Bad Request"
                  }
                }
              }
            }
          },
          "401": {
            "description": "인증 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 401,
                    "message": "유효하지 않거나 만료된 토큰입니다.",
                    "error": "Unauthorized"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "내 정보 수정",
        "tags": [
          "user"
        ]
      }
    },
    "/user/{id}": {
      "get": {
        "description": "특정 사용자의 정보를 반환합니다.",
        "operationId": "UserController_getOtherUserInfo",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "사용자의 정보 반환",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/MyInfoResponseDto"
                }
              }
            }
          },
          "400": {
            "description": "잘못된 요청 - 사용자 ID 형식이 잘못되었거나 누락됨",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 400,
                    "message": "잘못된 사용자 ID입니다.",
                    "error": "Bad Request"
                  }
                }
              }
            }
          },
          "404": {
            "description": "사용자 정보가 존재하지 않을 경우",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 404,
                    "message": "사용자 정보를 찾을 수 없습니다.",
                    "error": "Not Found"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "다른 사용자 정보 보기",
        "tags": [
          "user"
        ]
      }
    },
    "/user/me/project": {
      "get": {
        "description": "현재 인증된 사용자가 참여한 프로젝트 목록을 반환합니다. \"합격된\" 프로젝트만 포함됩니다.",
        "operationId": "UserController_getManyMyAcceptedProjects",
        "parameters": [],
        "responses": {
          "200": {
            "description": "사용자가 참여한 프로젝트 목록",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/ProjectResponseDto"
                  }
                }
              }
            }
          },
          "401": {
            "description": "인증 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 401,
                    "message": "유효하지 않거나 만료된 토큰입니다.",
                    "error": "Unauthorized"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "참여 프로젝트 조회 (내 프로젝트)",
        "tags": [
          "user"
        ]
      }
    },
    "/user/{id}/project": {
      "get": {
        "description": "특정 사용자가 참여한 프로젝트(합격)와 기획한 프로젝트를 반환합니다.",
        "operationId": "UserController_getManyUserAcceptedProjects",
        "parameters": [
          {
            "name": "id",
            "required": true,
            "in": "path",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "특정 사용자가 참여한 및 기획한 프로젝트 목록",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/UserProjectsResponseDto"
                }
              }
            }
          },
          "400": {
            "description": "잘못된 사용자 ID 요청",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 400,
                    "message": "잘못된 사용자 ID입니다.",
                    "error": "Bad Request"
                  }
                }
              }
            }
          },
          "401": {
            "description": "인증 실패",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 401,
                    "message": "유효하지 않거나 만료된 토큰입니다.",
                    "error": "Unauthorized"
                  }
                }
              }
            }
          },
          "404": {
            "description": "사용자 정보를 찾을 수 없음",
            "content": {
              "application/json": {
                "schema": {
                  "example": {
                    "statusCode": 404,
                    "message": "사용자를 찾을 수 없습니다.",
                    "error": "Not Found"
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "JWT": []
          }
        ],
        "summary": "참여 및 기획 프로젝트 조회 (특정 사용자)",
        "tags": [
          "user"
        ]
      }
    }
  },
  "info": {
    "title": "DevPals",
    "description": "DevPals API Docs",
    "version": "0.1",
    "contact": {}
  },
  "tags": [],
  "servers": [],
  "components": {
    "securitySchemes": {
      "JWT": {
        "scheme": "bearer",
        "bearerFormat": "JWT",
        "type": "http",
        "in": "header",
        "name": "JWT"
      }
    },
    "schemas": {
      "SignUpDto": {
        "type": "object",
        "properties": {
          "email": {
            "type": "string",
            "example": "devpals@mail.com",
            "description": "사용자의 이메일 주소"
          },
          "password": {
            "type": "string",
            "example": "test123!",
            "description": "사용자의 비밀번호"
          },
          "nickname": {
            "type": "string",
            "example": "김개발",
            "description": "사용자의 닉네임"
          }
        },
        "required": [
          "email",
          "password",
          "nickname"
        ]
      },
      "LoginDto": {
        "type": "object",
        "properties": {
          "email": {
            "type": "string",
            "example": "devpals@mail.com",
            "description": "사용자의 이메일 주소"
          },
          "password": {
            "type": "string",
            "example": "test123!",
            "description": "사용자의 비밀번호"
          }
        },
        "required": [
          "email",
          "password"
        ]
      },
      "ResetPasswordDto": {
        "type": "object",
        "properties": {
          "email": {
            "type": "string",
            "example": "devpals@mail.com",
            "description": "사용자의 이메일 주소"
          },
          "newPassword": {
            "type": "string",
            "example": "newPass123!",
            "description": "새로운 비밀번호"
          }
        },
        "required": [
          "email",
          "newPassword"
        ]
      },
      "SendEmailCodeDto": {
        "type": "object",
        "properties": {
          "email": {
            "type": "string",
            "example": "devpals@mail.com",
            "description": "사용자의 이메일 주소"
          }
        },
        "required": [
          "email"
        ]
      },
      "VerifyEmailCodeDto": {
        "type": "object",
        "properties": {
          "email": {
            "type": "string",
            "example": "devpals@mail.com",
            "description": "사용자의 이메일 주소"
          },
          "code": {
            "type": "string",
            "example": "123456",
            "description": "인증 코드"
          }
        },
        "required": [
          "email",
          "code"
        ]
      },
      "CareerDto": {
        "type": "object",
        "properties": {}
      },
      "CreateApplicantDTO": {
        "type": "object",
        "properties": {
          "email": {
            "type": "string",
            "example": "devpals@mail.com",
            "description": "지원자 이메일 주소"
          },
          "phoneNumber": {
            "type": "string",
            "example": "010-0000-0000",
            "description": "지원자 휴대폰 번호"
          },
          "message": {
            "type": "string",
            "example": "하고 싶은 말",
            "description": "뽑아주세요."
          },
          "career": {
            "description": "경력사항/수상이력",
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/CareerDto"
            }
          }
        },
        "required": [
          "email",
          "phoneNumber",
          "message"
        ]
      },
      "ModifyApplicantStatusDTO": {
        "type": "object",
        "properties": {
          "status": {
            "type": "string",
            "enum": [
              "ACCEPTED",
              "REJECTED",
              "WAITING"
            ],
            "description": "합격/불합격/대기 상태 선택"
          }
        },
        "required": [
          "status"
        ]
      },
      "CreateProjectDTO": {
        "type": "object",
        "properties": {
          "title": {
            "type": "string",
            "example": "클론코딩 사이드 프로젝트 모집 공고",
            "description": "공고 제목"
          },
          "description": {
            "type": "string",
            "description": "마크 다운 공고 내용"
          },
          "totalMember": {
            "type": "number",
            "example": 3,
            "description": "모집 인원"
          },
          "startDate": {
            "format": "date-time",
            "type": "string",
            "example": "2025-01-25",
            "description": "시작 예정일"
          },
          "estimatedPeriod": {
            "type": "string",
            "example": "3개월",
            "description": "예상 기간"
          },
          "methodId": {
            "type": "number",
            "example": 1,
            "description": "진행 방식 id"
          },
          "isBeginner": {
            "type": "boolean",
            "example": true,
            "description": "새싹 환영"
          },
          "recruitmentStartDate": {
            "format": "date-time",
            "type": "string",
            "example": "2025-01-06",
            "description": "모집 시작 날짜"
          },
          "recruitmentEndDate": {
            "format": "date-time",
            "type": "string",
            "example": "2025-02-15",
            "description": "모집 마감 날짜"
          },
          "skillTagId": {
            "example": [
              1,
              2
            ],
            "description": "스킬 태그",
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "positionTagId": {
            "example": [
              1,
              2
            ],
            "description": "포지션 태그",
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        },
        "required": [
          "title",
          "description",
          "totalMember",
          "startDate",
          "estimatedPeriod",
          "methodId",
          "isBeginner",
          "recruitmentStartDate",
          "recruitmentEndDate",
          "skillTagId",
          "positionTagId"
        ]
      },
      "ModifyProjectDTO": {
        "type": "object",
        "properties": {
          "title": {
            "type": "string",
            "example": "클론코딩 사이드 프로젝트 모집 공고",
            "description": "공고 제목"
          },
          "description": {
            "type": "string",
            "description": "마크 다운 공고 내용"
          },
          "totalMember": {
            "type": "number",
            "example": 3,
            "description": "모집 인원"
          },
          "startDate": {
            "format": "date-time",
            "type": "string",
            "example": "2025-01-25",
            "description": "시작 예정일"
          },
          "estimatedPeriod": {
            "type": "string",
            "example": "3개월",
            "description": "예상 기간"
          },
          "methodId": {
            "type": "number",
            "example": 1,
            "description": "진행 방식 id"
          },
          "isBeginner": {
            "type": "boolean",
            "example": true,
            "description": "새싹 환영"
          },
          "recruitmentStartDate": {
            "format": "date-time",
            "type": "string",
            "example": "2025-01-06",
            "description": "모집 시작 날짜"
          },
          "recruitmentEndDate": {
            "format": "date-time",
            "type": "string",
            "example": "2025-02-15",
            "description": "모집 마감 날짜"
          },
          "skillTagId": {
            "example": [
              1,
              2
            ],
            "description": "스킬 태그",
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "positionTagId": {
            "example": [
              1,
              2
            ],
            "description": "포지션 태그",
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        },
        "required": [
          "title",
          "description",
          "totalMember",
          "startDate",
          "estimatedPeriod",
          "methodId",
          "isBeginner",
          "recruitmentStartDate",
          "recruitmentEndDate",
          "skillTagId",
          "positionTagId"
        ]
      },
      "CheckNicknameDto": {
        "type": "object",
        "properties": {
          "nickname": {
            "type": "string",
            "description": "확인할 닉네임",
            "example": "devpals"
          }
        },
        "required": [
          "nickname"
        ]
      },
      "PositionDto": {
        "type": "object",
        "properties": {
          "id": {
            "type": "number",
            "description": "포지션 ID",
            "example": 2
          },
          "name": {
            "type": "string",
            "description": "포지션 이름",
            "example": "프론트엔드"
          }
        },
        "required": [
          "id",
          "name"
        ]
      },
      "SkillDto": {
        "type": "object",
        "properties": {
          "skillName": {
            "type": "string",
            "description": "스킬 이름",
            "example": "JavaScript"
          },
          "skillImg": {
            "type": "string",
            "description": "스킬 이미지 URL",
            "example": "https://example.com/js-logo.png"
          }
        },
        "required": [
          "skillName",
          "skillImg"
        ]
      },
      "MyInfoResponseDto": {
        "type": "object",
        "properties": {
          "id": {
            "type": "number",
            "description": "사용자 ID",
            "example": 1
          },
          "nickname": {
            "type": "string",
            "description": "사용자 닉네임",
            "example": "Jenny"
          },
          "email": {
            "type": "string",
            "description": "사용자 이메일",
            "example": "jenny@example.com"
          },
          "bio": {
            "type": "string",
            "description": "사용자 소개 (bio)",
            "example": "안녕하세요, 저는 프론트엔드 개발자입니다."
          },
          "profileImg": {
            "type": "string",
            "description": "사용자 프로필 이미지 URL",
            "example": "https://example.com/profile.jpg"
          },
          "userLevel": {
            "type": "string",
            "description": "사용자 레벨",
            "example": "Beginner"
          },
          "github": {
            "type": "string",
            "description": "GitHub 링크",
            "example": "https://github.com/jennywithlove"
          },
          "career": {
            "description": "경력사항/수상이력",
            "example": [
              {
                "name": "Google",
                "periodStart": "2020-01-01",
                "periodEnd": "2022-01-01",
                "role": "Software Engineer"
              },
              {
                "name": "Facebook",
                "periodStart": "2018-06-01",
                "periodEnd": "2019-12-31",
                "role": "Backend Developer"
              }
            ],
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/CareerDto"
            }
          },
          "positionTag": {
            "description": "포지션 태그 정보",
            "example": {
              "id": 2,
              "name": "프론트엔드"
            },
            "allOf": [
              {
                "$ref": "#/components/schemas/PositionDto"
              }
            ]
          },
          "skills": {
            "description": "사용자의 스킬셋",
            "example": [
              {
                "skillName": "JavaScript",
                "skillImg": "https://example.com/js-logo.png"
              },
              {
                "skillName": "TypeScript",
                "skillImg": "https://example.com/TypeScript-logo.png"
              },
              {
                "skillName": "React",
                "skillImg": "https://example.com/react-logo.png"
              }
            ],
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/SkillDto"
            }
          },
          "createdAt": {
            "format": "date-time",
            "type": "string",
            "description": "사용자 생성일",
            "example": "2023-01-01T00:00:00.000Z"
          }
        },
        "required": [
          "id",
          "nickname",
          "email",
          "bio",
          "profileImg",
          "userLevel",
          "github",
          "career",
          "positionTag",
          "skills",
          "createdAt"
        ]
      },
      "UpdateUserDto": {
        "type": "object",
        "properties": {
          "nickname": {
            "type": "string",
            "description": "사용자 닉네임",
            "example": "newNickname"
          },
          "bio": {
            "type": "string",
            "description": "사용자 소개 (bio)",
            "example": "새로운 소개글입니다."
          },
          "github": {
            "type": "string",
            "description": "GitHub 링크",
            "example": "https://github.com/example"
          },
          "positionTagId": {
            "type": "number",
            "description": "포지션 태그 ID",
            "example": 2
          },
          "skillTagIds": {
            "description": "스킬 태그 ID 배열",
            "example": [
              1,
              2,
              3
            ],
            "type": "array",
            "items": {
              "type": "number"
            }
          },
          "career": {
            "description": "경력사항/수상이력",
            "example": [
              {
                "name": "Google",
                "periodStart": "2020-01-01",
                "periodEnd": "2022-01-01",
                "role": "Software Engineer"
              },
              {
                "name": "Facebook",
                "periodStart": "2018-06-01",
                "periodEnd": "2019-12-31",
                "role": "Backend Developer"
              }
            ],
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/CareerDto"
            }
          }
        },
        "required": [
          "nickname",
          "bio",
          "github",
          "positionTagId",
          "skillTagIds",
          "career"
        ]
      },
      "SkillTagDto": {
        "type": "object",
        "properties": {
          "id": {
            "type": "number",
            "description": "스킬 태그 ID",
            "example": 1
          },
          "name": {
            "type": "string",
            "description": "스킬 태그 이름",
            "example": "JavaScript"
          },
          "img": {
            "type": "string",
            "description": "스킬 이미지 URL",
            "example": "https://example.com/js-logo.png"
          }
        },
        "required": [
          "id",
          "name",
          "img"
        ]
      },
      "ProjectSkillTagDto": {
        "type": "object",
        "properties": {
          "projectId": {
            "type": "number",
            "description": "프로젝트 ID",
            "example": 10
          },
          "skillTagId": {
            "type": "number",
            "description": "스킬 태그 ID",
            "example": 1
          },
          "SkillTag": {
            "description": "스킬 태그",
            "allOf": [
              {
                "$ref": "#/components/schemas/SkillTagDto"
              }
            ]
          }
        },
        "required": [
          "projectId",
          "skillTagId",
          "SkillTag"
        ]
      },
      "PositionTagDto": {
        "type": "object",
        "properties": {
          "id": {
            "type": "number",
            "description": "포지션 태그 ID",
            "example": 1
          },
          "name": {
            "type": "string",
            "description": "포지션 태그 이름",
            "example": "백엔드"
          }
        },
        "required": [
          "id",
          "name"
        ]
      },
      "ProjectPositionTagDto": {
        "type": "object",
        "properties": {
          "projectId": {
            "type": "number",
            "description": "프로젝트 ID",
            "example": 10
          },
          "positionTagId": {
            "type": "number",
            "description": "포지션 태그 ID",
            "example": 1
          },
          "PositionTag": {
            "description": "포지션 태그",
            "allOf": [
              {
                "$ref": "#/components/schemas/PositionTagDto"
              }
            ]
          }
        },
        "required": [
          "projectId",
          "positionTagId",
          "PositionTag"
        ]
      },
      "ProjectResponseDto": {
        "type": "object",
        "properties": {
          "projectId": {
            "type": "number",
            "description": "프로젝트 ID",
            "example": 10
          },
          "title": {
            "type": "string",
            "description": "프로젝트 제목",
            "example": "클론코딩 사이드 프로젝트 모집 공고"
          },
          "description": {
            "type": "string",
            "description": "프로젝트 설명",
            "example": "string"
          },
          "totalMember": {
            "type": "number",
            "example": 3,
            "description": "모집 인원"
          },
          "startDate": {
            "type": "string",
            "description": "프로젝트 시작 날짜",
            "example": "2025-01-25T00:00:00.000Z"
          },
          "estimatedPeriod": {
            "type": "string",
            "description": "예상 기간",
            "example": "3개월"
          },
          "methodId": {
            "type": "number",
            "description": "진행 방식 ID",
            "example": 1
          },
          "isBeginner": {
            "type": "boolean",
            "description": "초보자 참여 가능 여부",
            "example": true
          },
          "isDone": {
            "type": "boolean",
            "description": "프로젝트 마감 현황",
            "example": true
          },
          "recruitmentStartDate": {
            "type": "string",
            "description": "모집 시작 날짜",
            "example": "2025-01-06T00:00:00.000Z"
          },
          "recruitmentEndDate": {
            "type": "string",
            "description": "모집 마감 날짜",
            "example": "2025-02-15T00:00:00.000Z"
          },
          "status": {
            "type": "string",
            "description": "지원 상태",
            "example": "ACCEPTED"
          },
          "ProjectSkillTag": {
            "description": "프로젝트 스킬 태그 목록",
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/ProjectSkillTagDto"
            }
          },
          "ProjectPositionTag": {
            "description": "프로젝트 포지션 태그 목록",
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/ProjectPositionTagDto"
            }
          }
        },
        "required": [
          "projectId",
          "title",
          "description",
          "totalMember",
          "startDate",
          "estimatedPeriod",
          "methodId",
          "isBeginner",
          "isDone",
          "recruitmentStartDate",
          "recruitmentEndDate",
          "status",
          "ProjectSkillTag",
          "ProjectPositionTag"
        ]
      },
      "UserProjectsResponseDto": {
        "type": "object",
        "properties": {
          "acceptedProjects": {
            "description": "사용자가 참여한 프로젝트 목록",
            "example": [
              {
                "projectId": 1,
                "title": "참여한 프로젝트",
                "description": "참여한 프로젝트 설명",
                "totalMember": 5,
                "startDate": "2025-01-01T00:00:00.000Z",
                "estimatedPeriod": "3개월",
                "methodId": 1,
                "isBeginner": true,
                "isDone": true,
                "recruitmentStartDate": "2025-01-01T00:00:00.000Z",
                "recruitmentEndDate": "2025-02-01T00:00:00.000Z",
                "status": "ACCEPTED",
                "ProjectSkillTag": [],
                "ProjectPositionTag": []
              }
            ],
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/ProjectResponseDto"
            }
          },
          "ownProjects": {
            "description": "사용자가 기획한 프로젝트 목록",
            "example": [
              {
                "projectId": 2,
                "title": "기획한 프로젝트",
                "description": "기획한 프로젝트 설명",
                "totalMember": 3,
                "startDate": "2025-03-01T00:00:00.000Z",
                "estimatedPeriod": "6개월",
                "methodId": 2,
                "isBeginner": false,
                "isDone": true,
                "recruitmentStartDate": "2025-02-01T00:00:00.000Z",
                "recruitmentEndDate": "2025-04-01T00:00:00.000Z",
                "ProjectSkillTag": [],
                "ProjectPositionTag": []
              }
            ],
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/ProjectResponseDto"
            }
          }
        },
        "required": [
          "acceptedProjects",
          "ownProjects"
        ]
      }
    }
  }
};  // JSON 데이터를 직접 삽입
            const ui = SwaggerUIBundle({
                spec: spec,
                dom_id: '#swagger-ui',
                deepLinking: true,
                presets: [SwaggerUIBundle.presets.apis, SwaggerUIStandalonePreset],
                layout: "BaseLayout"
            });
            window.ui = ui;
        };
    </script>
</body>
</html>
