# form-ant-dynamic Form


      import React from "react";
      import { CloseOutlined } from "@ant-design/icons";
      import { Button, Card, Form, Input, Space, Typography } from "antd";
      
      const LoginCmp = () => {
        const [form] = Form.useForm();
      
        const onFinish = (values) => {
          console.log("Received values of form:", values);
        };
      
        return (
          <Form
            labelCol={{
              span: 6,
            }}
            wrapperCol={{
              span: 18,
            }}
            form={form}
            name="dynamic_form_complex"
            style={{
              maxWidth: 600,
            }}
            autoComplete="off"
            initialValues={{
              items: [{}],
            }}
            onFinish={onFinish}
          >
            <Form.Item
              label="Username"
              name="username"
              rules={[
                {
                  required: true,
                  message: "Please input your username!",
                },
              ]}
            >
              <Input />
            </Form.Item>
      
            <Form.List name="items">
              {(fields, { add, remove }) => (
                <div
                  style={{
                    display: "flex",
                    rowGap: 16,
                    flexDirection: "column",
                  }}
                >
                  {fields.map((field) => (
                    <Card
                      size="small"
                      title={`Item ${field.name + 1}`}
                      key={field.key}
                      extra={
                        field.name > 0 && (
                          <CloseOutlined
                            onClick={() => {
                              if (field.name > 0) remove(field.name);
                            }}
                          />
                        )
                      }
                    >
                      <Form.Item
                        label="Name"
                        rules={[
                          {
                            required: true,
                          },
                        ]}
                        name={[field.name, "name"]}
                      >
                        <Input />
                      </Form.Item>
                    </Card>
                  ))}
      
                  <Button type="dashed" onClick={() => add()} block>
                    + Add Item
                  </Button>
                </div>
              )}
            </Form.List>
      
            <Form.Item>
              <Button danger htmlType="submit">
                button Submit
              </Button>
            </Form.Item>
          </Form>
        );
      };
      export default LoginCmp;
